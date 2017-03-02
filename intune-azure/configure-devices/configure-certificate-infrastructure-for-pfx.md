---
title: "PKCS の Intune 証明書インフラストラクチャを構成する | Intune Azure プレビュー | Microsoft Docs"
description: "Intune Azure プレビュー: Intune で PKCS 証明書を使用するようにインフラストラクチャを構成する方法について説明します。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: e189ebd1-6ca1-4365-9d5d-fab313b7e979
ms.reviewer: vinaybha
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4d095506215b775d56d172e9aabae1737757310
ms.openlocfilehash: 6f08dc63a9afaa5e92b188883d160d0b76f3631f
ms.lasthandoff: 02/16/2017



---
# <a name="configure-your-microsoft-intune-certificate-infrastructure-for-pkcs"></a>PKCS の Microsoft Intune 証明書インフラストラクチャを構成する
[!INCLUDE[azure_preview](../includes/azure_preview.md)]

このトピックでは、Intune で PKCS 証明書プロファイルを作成して展開するために必要なものについて説明します。

組織で証明書ベースの認証を行うには、エンタープライズ証明機関が必要です。

また、PKCS 証明書プロファイルを使用するには、エンタープライズ証明機関に加えて次のものが必要です。

-   証明機関と通信できるコンピューターまたは証明機関コンピューター自体を使用します。

-  証明機関と通信できるコンピューターで実行する Intune 証明書コネクタ。

## <a name="important-terms"></a>重要な用語


-    **Active Directory ドメイン**: このセクションで示されているすべてのサーバー (Web アプリケーション プロキシ サーバーを除く) は、Active Directory ドメインに参加する必要があります。

-  **証明機関**: Windows Server 2008 R2 以降の Enterprise エディションで実行するエンタープライズ証明機関 (CA) が必要です。 スタンドアロン CA はサポートされません。 証明機関をセットアップする方法の詳細については、 [証明機関のインストールに関するページ](http://technet.microsoft.com/library/jj125375.aspx)を参照してください。
    CA が Windows Server 2008 R2 を搭載している場合は、 [KB2483564 の修正プログラムをインストール](http://support.microsoft.com/kb/2483564/)する必要があります。

-  **証明機関と通信できるコンピューター**: 証明機関コンピューター自体を使用することもできます。
-  **Microsoft Intune 証明書コネクタ**: Azure Portal から**証明書コネクタ** インストーラー (**ndesconnectorssetup.exe**) をダウンロードします。 これにより、証明書コネクタをインストールするコンピューターで **ndesconnectorssetup.exe** を実行できます。 PKCS 証明書プロファイルの場合は、証明機関と通信するコンピューターに証明書コネクタをインストールします。
-  **Web アプリケーション プロキシ サーバー** (省略可能): Web アプリケーション プロキシ (WAP) サーバーとして Windows Server 2012 R2 以降を実行しているサーバーを使用できます。 この構成は:
    -  デバイスはインターネット接続を使用して証明書を受信できます。
    -  デバイスがインターネット接続経由で証明書を受信して更新する場合のセキュリティ推奨事項です。

 > [!NOTE]           
> -    WAP をホストするサーバーは、ネットワーク デバイス登録サービス (NDES) で使用される長い URL のサポートを有効にする[更新プログラムをインストールする](http://blogs.technet.com/b/ems/archive/2014/12/11/hotfix-large-uri-request-in-web-application-proxy-on-windows-server-2012-r2.aspx) 必要があります。 この更新プログラムは、 [2014 年 12 月の更新プログラムのロールアップ](http://support.microsoft.com/kb/3013769)に含まれます。または、 [KB3011135](http://support.microsoft.com/kb/3011135)から個別に入手できます。
>-  また、WAP をホストするサーバーが、外部クライアントに公開される名前と一致する SSL 証明書を持ち、NDES サーバーで使用される SSL 証明書を信頼する必要があります。 これらの証明書を使用すると、WAP サーバーはクライアントからの SSL 接続を終了し、NDES サーバーへの新しい SSL 接続を作成できます。
    WAP の証明書については、「[内部アプリケーションの公開のために Web アプリケーション プロキシをインストールおよび構成する](https://technet.microsoft.com/library/dn383650.aspx)」の**証明書の計画**に関するセクションを参照してください。 WAP サーバーの一般的な情報については、「[Web アプリケーション プロキシの使用](http://technet.microsoft.com/library/dn584113.aspx)」を参照してください。|


## <a name="certificates-and-templates"></a>証明書とテンプレート

|オブジェクト|説明|
|----------|-----------|
|**証明書テンプレート**|発行元 CA でこのテンプレートを構成します。|
|**信頼されたルート CA 証明書**|これを発行元 CA または発行元 CA を信頼するデバイスから **.cer** ファイルとしてエクスポートし、信頼された CA 証明書プロファイルを使用してデバイスに展開します。<br /><br />オペレーティング システムのプラットフォームごとに&1; つの信頼されたルート CA 証明書を使用し、作成する各信頼されたルート証明書プロファイルに関連付けます。<br /><br />必要に応じて、信頼されたルート CA 証明書を追加して使用できます。 ルート CA 証明書を追加する局面としては、Wi-Fi アクセス ポイント用のサーバー認証証明書に署名する CA の信頼性を担保する必要がある場合などが考えられます。|


## <a name="configure-your-infrastructure"></a>インフラストラクチャを構成する
証明書プロファイルを構成するには、次のタスクを完了する必要があります。 以下のタスクには、Windows Server 2012 R2 と Active Directory 証明書サービス (ADCS) についての知識が必要となります。

- **タスク 1** - 証明機関で証明書テンプレートを構成する。
- **タスク 2** - Intune 証明書コネクタを有効にし、インストールし、構成する。

## <a name="task-1---configure-certificate-templates-on-the-certification-authority"></a>タスク 1 - 証明機関で証明書テンプレートを構成する
このタスクでは、証明書テンプレートを公開します。

### <a name="to-configure-the-certification-authority"></a>証明機関を構成するには

1.  発行元 CA で、証明書テンプレート スナップインを使用して、新しいカスタム テンプレートを作成するか、または PKCS で使用するために (ユーザー テンプレートのように) 既存のテンプレートをコピーして編集します。

    テンプレートには以下を含む必要があります。

    -   テンプレートのわかりやすい **テンプレート表示名** を指定します。

    -   [ **サブジェクト名** ] タブで [ **要求に含まれる**] を選択します (セキュリティが NDES の Intune ポリシー モジュールによって適用されます)。

    -   [ **拡張** ] タブで、[ **アプリケーション ポリシーの説明** ] に [ **クライアント認証**] が含まれることを確認します。

        > [!IMPORTANT]
        > iOS および Mac OS X の証明書テンプレートの場合、**[拡張]** タブで、**[キー使用法]** を編集し、**[署名は発行元の証明である]** がオンになっていないことを確認します。

2.  [ **一般** ] タブでテンプレートの [ **有効期間** ] を確認します。 既定では、Intune はテンプレートで構成されている値を使用します。 ただし、要求元が異なる値を指定できるように CA を構成できます。異なる値は、Intune 管理者コンソールから設定できます。 常にテンプレートの値を使用する場合は、この手順の残りの部分をスキップします。

    > [!IMPORTANT]
    > iOS および Mac OS X プラットフォームは、他の構成に関係なく、常にテンプレートで設定される値を使用します。

    要求元が有効期間を指定できるように CA を構成するには、CA で次のコマンドを実行します。

    a.  **certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**

    b.  **net stop certsvc**

    c.  **net start certsvc**

3.  発行元 CA で、証明機関スナップインを使用して証明書テンプレートを発行します。

    a.  **[証明書テンプレート]** ノードを選択し、**[アクション]** -&gt; **[新規]** &gt; **[発行する証明書テンプレート]** の順にクリックして、手順 2. で作成したテンプレートを選択します。

    b.  [ **証明書テンプレート** ] フォルダーに表示されることで、テンプレートが発行されたことを確認します。

4.  CA コンピューターで、Intune 証明書コネクタをホストするコンピューターが、PKCS 証明書プロファイルの作成で使用するテンプレートにアクセスできるように、登録アクセス許可を持つことを確認します。 CA コンピューター プロパティの **[セキュリティ]** タブでそのアクセス許可を設定します。

## <a name="task-2---enable-install-and-configure-the-intune-certificate-connector"></a>タスク 2 - Intune 証明書コネクタを有効にし、インストールし、構成する
このタスクでは次のことを行います。

証明書コネクタをダウンロードし、インストールして、構成します。

### <a name="to-enable-support-for-the-certificate-connector"></a>証明書コネクタのサポートを有効にするには

1.  Azure ポータルにサインインします。
2.  **[その他のサービス]** > **[その他]** > **[Intune]** の順に選択します。
3.  **[Intune]** ブレードで、**[デバイスの構成]** を選択します。
2.  **[デバイス構成]** ブレードで、**[セットアップ]** > **[証明機関]** の順に選択します。
2.  **[手順 1]** で、**[有効にする]** を選択します。

### <a name="to-download-install-and-configure-the-certificate-connector"></a>証明書コネクタをダウンロードし、インストールして、構成するには

1.  **[デバイスの構成]** ブレードで、**[セットアップ]** > **[証明機関]** の順に選択します。
2.  **[Certificate Connector のダウンロード]** を選択します。
2.  ダウンロードが完了したら、ダウンロードされたインストーラー (**ndesconnectorssetup.exe**) を実行します。
  証明機関と接続できるコンピューターでインストーラーを実行します。 [PKCS (.PFX) の配布] オプションを選択し、**[インストール]** を選択します。 インストールが完了したら、[証明書プロファイルを構成する方法](how-to-configure-certificates.md)に関するページの説明に従って、証明書プロファイルを作成して続行します。

3.  証明書コネクタのクライアント証明書の入力を求められたら、**[選択]** を選択し、インストールした**クライアント認証**証明書を選択します。

    クライアント認証証明書を選択した後、[ **Microsoft Intune 証明書コネクタのクライアント証明書** ] 画面に戻ります。 選択した証明書は表示されませんが、**[次へ]** を選択してその証明書のプロパティを表示します。 **[次へ]** を選択して、**[インストール]** を選択します。

4.  ウィザードが完了した後、ウィザードを閉じる前に、[ **証明書コネクタの UI を起動**] をクリックします。

    > [!TIP]
    > 証明書コネクタの UI を起動する前にウィザードを閉じた場合は、次のコマンドを実行して再び開くことができます。
    >
    > **&lt;install_Path&gt;\NDESConnectorUI\NDESConnectorUI.exe**

5.  **証明書コネクタ** UI で:

    a. **[サインイン]** を選択し、Intune サービス管理者の資格情報、またはグローバル管理アクセス許可を持つテナント管理者の資格情報を入力します。

  <!--  If your organization uses a proxy server and the proxy is needed for the NDES server to access the Internet, click **Use proxy server** and then provide the proxy server name, port, and account credentials to connect.-->

    b. **[詳細設定]** タブを選択し、発行元 CA で**証明書の発行と管理**アクセス許可を持つアカウントの資格情報を指定します。

    c. **[適用]** を選択します。

    これで、証明書コネクタ UI を閉じることができます。

6.  コマンド プロンプトを開き、**services.msc** を入力します。 **[Enter]** キーを押し、**[Intune コネクタ サービス]** を右クリックして、**[再起動]** を選択します。

サービスが実行していることを確認するには、ブラウザーを開き、次の URL を入力します。 **403** エラーが返る必要があります。

**http:// &lt;FQDN_of_your_NDES_server&gt;/certsrv/mscep/mscep.dll**

### <a name="next-steps"></a>次のステップ
これで、[Microsoft Intune で証明書を構成する方法](how-to-configure-certificates.md)に関するページの説明に従って、証明書プロファイルを設定する準備が整いました。
