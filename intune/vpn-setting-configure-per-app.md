---
title: Microsoft Intune での iOS デバイスに対するアプリごとの VPN の設定 - Azure | Microsoft Docs
description: 前提条件を参照し、仮想プライベート ネットワーク (VPN) ユーザーのグループを作成し、SCEP 証明書プロファイルを追加し、アプリごとの VPN プロファイルを構成し、iOS デバイスの Microsoft Intune でいくつかのアプリを VPN プロファイルに割り当てます。 デバイスの VPN 接続を確認する手順も一覧表示します。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/28/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: karanda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 12131fe0b78814850cfadee15533620dd5813f6c
ms.sourcegitcommit: e9ba1280b95565a5c5674b825881655d0303e688
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2019
ms.locfileid: "54297402"
---
# <a name="set-up-per-app-virtual-private-network-vpn-in-intune-for-ios-devices"></a>Intune での iOS デバイス用のアプリごとの Virtual Private Network (VPN) 設定

管理対象のどのアプリが Intune で管理される iOS デバイスで仮想プライベート ネットワーク (VPN) を使用できるかを指定することができます。 Intune でアプリごとの VPN を作成すると、エンド ユーザーが会社のドキュメントにアクセスするときに自動的に VPN を通して接続します。

現在のところ、アプリごとの VPN は次のプロバイダーで利用できます。

 - Check Point Remote Access VPN
 - Cisco AnyConnect
 - Citrix
 - F5
 - Pulse Connect Secure
 - Palo Alto Networks
 - SonicWall
 - Zscaler プライベート アクセス

## <a name="prerequisites-for-per-app-vpn"></a>アプリごとの VPN の前提条件

> [!IMPORTANT]
> VPN ベンダーには、特定のハードウェアやライセンスなど、アプリごとの VPN に関する他の特定の要件がある場合があります。 必ず、そのドキュメントを参照し、Intune でアプリごとの VPN を設定する前に前提条件を満たすようにしてください。

身元を証明するため、VPN サーバーはデバイスによってプロンプトなしに受け入れられる必要がある証明書を提示します。 証明書の自動承認を確実に行うため、証明機関 (CA) によって発行された VPN サーバーのルート証明書を含む、信頼済み証明書プロファイルを作成します。 

証明書をエクスポートし、CA を追加します。

1. VPN サーバーの管理コンソールを開きます。
2. VPN サーバーが証明書ベースの認証を使用することを確認します。 
3. 信頼されたルート証明書ファイルをエクスポートします。 拡張子は .cer で、信頼済み証明書プロファイルの作成時にこのファイルを追加します。
4. VPN サーバーへの認証用に証明書を発行した CA の名前を追加します。
    デバイスによって提示される CA が VPN サーバーの信頼された証明機関リストのいずれかの CA と一致する場合、VPN サーバーによるデバイスの認証が成功します。

## <a name="create-a-group-for-your-vpn-users"></a>VPN ユーザーのグループを作成する

アプリごとの VPN にアクセスできるメンバーが含まれるように、Azure Active Directory (Azure AD) でグループを作成するか既存のグループを選択します。

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[すべてのサービス]** を選択し、**[Intune]** をフィルターとして適用し、**[Microsoft Intune]** を選択します。
2. **[グループ]** を選択し、**[新しいグループ]** をクリックします。
3. このグループの **[グループの種類]** を選択します。 
3. グループの **[グループ名]** を入力します。 
4. グループの **[グループの説明]** を入力します。 
5. **[メンバーシップの種類]** に **[割り当て済み]** を選択します。
7. **[メンバー]** ウィンドウで、名前またはメール アドレスで VPN ユーザーを検索します。
8. 各ユーザーを選択し、**[選択]** をクリックします。
9. **[作成]** をクリックします。

## <a name="create-a-trusted-certificate-profile"></a>信頼済み証明書プロファイルを作成する

CA によって発行された VPN サーバーのルート証明書を、Intune で作成されたプロファイルにインポートします。 信頼済み証明書プロファイルから iOS デバイスに、VPN サーバーが提示する CA を自動的に信頼するように指示します。

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[すべてのサービス]** を選択し、**[Intune]** をフィルターとして適用し、**[Microsoft Intune]** を選択します。
2. **[デバイス構成]** を選択して、**[プロファイル]** をクリックします。
3. **[プロファイルの作成]** をクリックします。 **[プロファイルの作成]** で、次の操作を実行します。
    1. **[名前]** を入力します。
    2. **[説明]** を入力します。
    3. **[プラットフォーム]** に **[iOS]** を選択します。
    4. **[プロファイルの種類]** に **[信頼できる証明書]** を選択します。
4. フォルダー アイコンをクリックし、VPN 管理コンソールからエクスポートした VPN 証明書 (.cer ファイル) を参照します。 **[OK]** をクリックします。
5. **[作成]** をクリックします。

    ![信頼済み証明書プロファイルを作成する](./media/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-certificate-profile"></a>SCEP 証明書プロファイルを作成する

信頼済みルート証明書プロファイルにより、iOS が VPN サーバーを自動的に信頼できるようになります。 SCEP 証明書は、iOS の VPN クライアントから VPN サーバーに資格情報を提供します。 この証明書により、iOS デバイスのユーザーにユーザー名とパスワードを求めることなく自動的にデバイスが認証できるようになります。 

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[すべてのサービス]** を選択し、**[Intune]** をフィルターとして適用し、**[Microsoft Intune]** を選択します。
2. **[デバイス構成]** を選択して、**[プロファイル]** をクリックします。
3. **[プロファイルの作成]** をクリックします。 **[プロファイルの作成]** で、次の操作を実行します。
    1. **[名前]** を入力します。
    2. **[説明]** を入力します。
    3. **[プラットフォーム]** に **[iOS]** を選択します。
    4. **[プロファイルの種類]** に **[SCEP 証明書]** を選択します。
4. **[証明書の有効期間]** に **[年]** を選択して、`2` を入力します。
5. **[サブジェクト名の形式]** に **[共通名]** を選択します。
6. **[サブジェクトの別名]** に **[ユーザー プリンシパル名 (UPN)]** を選択します。
7. **[キー使用法]** に **[デジタル署名]** および **[キーの暗号化]** を選択します。
8. **[キー サイズ (ビット)]** に **[2048]** を選択します。
9. ルート証明書をクリックし、SCEP 証明書を選択します。 **[OK]** をクリックします。
10. **[拡張キー使用法]** の **[名前]** に `Client Authentication` を入力します。
11. **[オブジェクト識別子]** に `1.3.6.1.5.5.7.3.2`を入力します。
12. **[追加]** をクリックします。
13. ***サーバーの URL*** を入力して、**[追加]** をクリックします。
14. **[OK]** をクリックします。
15. **[作成]** をクリックします。

    ![SCEP 証明書プロファイルを作成する](./media/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>アプリごとの VPN プロファイルを作成する

VPN プロファイルには、クライアントの資格情報を含む SCEP 証明書、VPN への接続情報、iOS アプリケーションがアプリごとの VPN 機能を使用できるようにする、アプリごとの VPN フラグが含まれています。

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[すべてのサービス]** を選択し、**[Intune]** をフィルターとして適用し、**[Microsoft Intune]** を選択します。
2. **[デバイス構成]** を選択して、**[プロファイル]** をクリックします。
3. **[プロファイルの作成]** をクリックします。 **[プロファイルの作成]** で、次の操作を実行します。
    1. **[名前]** を入力します。
    2. **[説明]** を入力します。
    3. **[プラットフォーム]** に **[iOS]** を選択します。
    4. **[プロファイルの種類]** に **[VPN]** を選択します。
4. **[基本 VPN]** を選択します。 **[基本 VPN]** で、次の操作を実行します。
    1. **[接続名]** を入力します。
    2. **[IP アドレスまたは FQDN]** を入力します。
    3. **[認証方法]** に **[証明書]** を選択します。
    4. **[認証証明書]** で SCEP 証明書を選択して、**[OK]** をクリックします。
    5. **[接続の種類]** に VPN を選択します。
    6. 必要に応じて、VPN の属性を構成します。
    7. **[分割トンネリング]** に [無効化] を選択します。
5. **[自動 VPN]** をクリックします。 **[自動 VPN]** で、次の操作を実行します。
    1. **[自動 VPN の種類]** に **[アプリごとの VPN]** を選択します。
    2. VPN の URL を入力して、**[追加]** をクリックします。
    3. **[OK]** をクリックします。
6. **[OK]** をクリックします。
7. **[作成]** をクリックします。

    ![アプリごとの VPN プロファイルを作成する](./media/vpn-per-app-create-vpn-profile.png)


## <a name="associate-an-app-with-the-vpn-profile"></a>アプリと VPN プロファイルを関連付ける

VPN プロファイルを追加した後、アプリと Azure AD グループをプロファイルに関連付けます。

1. [Azure ポータル](https://portal.azure.com) にサインインします。
2. **[すべてのサービス]** を選択し、**[Intune]** をフィルターとして適用し、**[Microsoft Intune]** を選択します。
3. **[クライアント アプリ]** を選択します。
4. **[アプリ]** をクリックします。
5. アプリの一覧からアプリを選択します。
6. **[割り当て]** をクリックします。
7. **[グループの追加]** をクリックします。
8. **[グループの追加]** ウィンドウの **[割り当ての種類]** に **[必須]** を選択します。
9. 前に定義したグループを選択して、**[Make this app required]\(このアプリを必須にします\)** を選択します。
10. **[VPN]** に VPN 定義を選択します。
 
    > [!NOTE]  
    > VPN 定義が値を取得するまで、1 分程度かかる場合があります。 3 - 5 分間待ってから、**[保存]** をクリックします。

11. **[OK]** をクリックし、**[保存]** をクリックします。

    ![アプリと VPN を関連付ける](./media/vpn-per-app-app-to-vpn.png)

アプリとプロファイルの関連付けは、次の条件が存在する場合、次回のデバイス チェックインの際に解除されます。
- アプリが必須インストール インテントのターゲットになった場合
- プロファイルとアプリの両方が同じグループをターゲットにしている場合
- アプリごとの VPN 構成をアプリ割り当てから削除する場合

次の条件がある場合、アプリとプロファイルの関連付けは、エンドユーザーが会社のポータルからの再インストールを要求するまで存在します。
- アプリが利用可能インストール インテントのターゲットになった場合
- プロファイルとアプリの両方が同じグループをターゲットにしている場合
- エンド ユーザーが会社のポータルでアプリのインストールを要求したため、アプリとプロファイルがデバイスにインストールされる場合
- アプリごとの VPN 構成をアプリ割り当てから削除または変更する場合

## <a name="verify-the-connection-on-the-ios-device"></a>iOS デバイスでの接続を確認する

アプリと関連付けられたアプリごとの VPN 設定で、デバイスからの接続を確認します。

### <a name="before-you-attempt-to-connect"></a>接続を試行する前に

 - iOS 9 以降を実行していることを確認します。
 - 同じユーザーのグループに、前述の*すべての*ポリシーを展開しておきます。 展開されていないと、アプリごとの VPN がほぼ確実に中断します。  
 - サポートされているサード パーティ製 VPN アプリがインストールされていることを確認します。 次の VPN アプリがサポートされています。
    - Check Point Capsule Connect
    - Cisco AnyConnect
    - Citrix VPN
    - Citrix SSO
    - F5 Access
    - Palo Alto Networks GlobalProtect
    - Pulse Secure
    - SonicWall Mobile Connect
    - Zscaler

    > [!NOTE]
    > Pulse Secure VPN アプリを使用している場合、アプリ層またはパケット層でのトンネリングを使用することを選択できます。 **[ProviderType]** 値に、アプリ層トンネリングには **[app-proxy]** を設定し、パケット層トンネリングには **[packet-tunnel]** を設定します。

### <a name="connect-using-the-per-app-vpn"></a>アプリごとの VPN を使用して接続する

VPN を選択したり、資格情報を入力したりせずに接続されるゼロタッチ操作を確認します。 ゼロタッチ操作とは、次のような意味です。

 - デバイスから VPN サーバーを信頼するように求められません。 つまり、**[Dynamic Trust]\(動的な信頼\)** ダイアログ ボックスが表示されます。
 - 資格情報を入力する必要はありません。
 - [接続] ボタンをタップすると、VPN に接続します。

iOS デバイスで接続を確認します。

1. VPN アプリをタップします。
2. **[接続]** をタップします。  
VPN は、余分なプロンプトを表示せずに正常に接続します。

<!-- ## Troubleshooting the per-app VPN

The user experiences the feature by silently connecting to the VPN. This experience, however, can provide little information for troubleshooting. You can review the event logs crated by the iOS device.

`Note -- use the Apple Configurator as the supported tool. Only runs on a mac.'

To review event logs:

1. Connect your iOS device to a PC
2. Open the **iPhone Configuration Utility** (IPCU). If you do not have a copy, you can install it from [CompatCenter](http://www.microsoft.com/en-us/windows/compatibility/CompatCenter/ProductDetailsViewer?Name=iPhone%20Configuration%20Utility&vendor=Apple&Locale=1033%2C2057%2C3081%2C4105%2C16393&ModelOrVersion=3&BreadCrumbPath=iphone%20configuration%20utility&LastSearchTerm=iphone%2Bconfiguration%2Butility&Type=Software&tempOsid=Windows%208.1)
3. Review the logs. -->

## <a name="next-steps"></a>次の手順

- iOS 設定を確認するには、「[Microsoft Intune での iOS デバイス向けの VPN 設定](vpn-settings-ios.md)」を参照してください。
-  VPN の設定と Intune の詳細については、「[Microsoft Intune で VPN の設定を構成する方法](vpn-settings-configure.md)」を参照してください。
