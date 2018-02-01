---
title: "iOS 用 Intune のデバイス シングル サインオンを構成する"
titlesuffix: Azure portal
description: "iOS デバイスのシングル サインオン用に Intune を構成します。"
keywords: 
author: vhorne
ms.author: victorh
manager: dougeby
ms.date: 12/7/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 07ac355232c1e4ac290c87191d3764e3df45327e
ms.sourcegitcommit: 4509039cbfd4d450324a3475fb5841906720baa1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2018
---
# <a name="configure-intune-for-ios-device-single-sign-on"></a>iOS 用 Intune のデバイス シングル サインオンを構成する

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

ほとんどの基幹業務 (LOB) アプリでは、セキュリティに対応するために、何らかのレベルのユーザー認証が必要です。 多くの場合、ユーザーはそのために同じ資格情報を何回も入力する必要があり、ストレスを感じることがあります。 ユーザーの操作環境を改善するため、開発者はシングル サインオンを使うアプリを作成し、ユーザーが資格情報を入力する必要のある回数を減らすことができます。

iOS デバイスのシングル サインオンを利用するには、次の条件が満たされている必要があります。

- iOS デバイス上のシングル サインオン ペイロードでユーザー資格情報ストアを探すようにアプリがコーディングされていること。
- iOS デバイスのシングル サインオン用に Intune が構成されていること。

## <a name="to-configure-intune-for-ios-device-single-sign-on"></a>iOS デバイスのシングル サインオン用に Intune を構成するには


1. サインイン、 [Azure ポータル](https://portal.azure.com)します。
2. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[デバイス構成]** を選択します。
2. **[デバイス構成]** ブレードで、**[プロファイル]** を選びます。
3. プロファイル ブレードで **[プロファイルの作成]** を選び、名前と説明を指定して、以下の設定を構成します。
   - **[プラットフォーム]**: **[iOS]** を選びます。 
   - **[プロファイルの種類]**: **[デバイス機能]** を選びます。
4. **[デバイス機能]** ブレードで、**[シングル サインオン]** を選びます。

   ![[シングル サインオン] ブレード](./media/sso-blade.png)

2. 次の表にまとめた情報を参考にして、**[シングル サインオン]** ブレードのフィールドを設定します。 詳しくは、表の後の説明をご覧ください。
   
   |フィールド  |注|
   |---------|---------|
   |**AAD からのユーザー名の属性**|デバイスにインストールされる XML ペイロードを生成する前に、Intune が AAD で各ユーザーについて調べて対応するフィールド (UPN など) に設定する属性です。|
   |**領域**|URL のドメイン部分です。|
   |**シングル サインオンを使用する URL プレフィックス**|ユーザーのシングル サインオン認証を必要とする、組織内の URL です。|
   |**シングル サインオンを使用するアプリ**|シングル サインオン ペイロードを使用する、エンド ユーザーのデバイス上のアプリです。|
   |**資格情報更新証明書**|認証に資格情報を使う場合は、認証証明書としてユーザーに展開される SCEP または PFX 証明書を選びます。|

以下のセクションでは、各シングル サインオン フィールドについて詳しく説明します。

### <a name="username-attribute-from-aad-and-realm"></a>AAD からのユーザー名の属性と領域

- このフィールドに対して **[ユーザー原則名]** を選ぶと、次のような方法で解析されます。

   ![ユーザー名属性](media/User-name-attribute.png)

   また、**[領域]** テキスト ボックスに入力したテキストで領域を上書きすることもできます。

   たとえば、Contoso にはヨーロッパ、アジア、北米などのサブ領域があり、 アジアのユーザーは SSO ペイロードを使って、アプリは *username@asia.contoso.com* の形式の UPN を要求するものとします。この場合、**[ユーザー原則名]** を選ぶと、既定で各ユーザーの領域は AAD から取得されますが、それは単に *contoso.com* のようなものかもしれません。そのため、アジアのユーザーについては、このペイロードを作成し、領域を値 *asia.contoso.com* で上書きすることができます。結果として、エンド ユーザーの UPN は、*username@contoso.com* ではなく *username@asia.contoso.com* になります。

- **[デバイス ID]** を選ぶと、Intune は自動的に Intune デバイス ID を選びます。

   既定では、アプリで使う必要があるのはデバイス ID だけです。 ただし、アプリがデバイス ID に加えて領域を使う場合は、**[領域]** テキスト ボックスに領域を入力できます。

   > [!NOTE]
   > 既定では、デバイス ID を使う場合は領域を空のままにします。

### <a name="url-prefixes-that-will-use-single-sign-on"></a>シングル サインオンを使用する URL プレフィックス

組織に存在していてユーザー認証を必要とする URL をここに入力します。

たとえば、ユーザーがそのようなサイトに接続すると、iOS デバイスはシングル サインオンの資格情報を使うので、ユーザーは資格情報をさらに入力する必要がありません。 ただし、多要素認証が有効になっている場合は、ユーザーは第 2 の認証情報を入力する必要があります。

> [!NOTE]
> これらの URL は、適切な形式の FQDN である必要があります。 Apple で要求されている形式は `http://<yourURL.domain>` です。

URL の一致パターンは、`http://` または `https://` で始まっている必要があります。 単純な文字列一致が実行されるので、URL プレフィックス `http://www.contoso.com/` は `http://www.contoso.com:80/` とは一致しません。 ただし、iOS 9.0 以降では、単一のワイルドカード * を使って、一致するすべての値を指定できます。 たとえば、`http://*.contoso.com/` は `http://store.contoso.com/` と `http://www.contoso.com` の両方と一致します。
パターン `http://.com` はすべての HTTP URL と一致し、`https://.com` はすべての HTTPS URL と一致します。

### <a name="apps-that-will-use-single-sign-on"></a>シングル サインオンを使用するアプリ

エンド ユーザーのデバイス上のアプリで、シングル サインオン ペイロードを使うことができるものを示します。

`AppIdentifierMatches` 配列には、アプリ バンドル ID と一致する文字列が含まれる必要があります。 これらの文字列では、完全に一致する値 (例: `com.contoso.myapp`) を指定するか、ワイルドカード文字 *\ を使ってバンドル ID のプレフィックス一致を指定することができます。 ワイルドカード文字は、ピリオド文字 (.) の後に指定する必要があり、文字列の最後で 1 回だけ使えます (例: `com.contoso.*`)。 ワイルドカードが含まれる場合は、バンドル ID がプレフィックスで始まるすべてのアプリが、アカウントへのアクセスを許可されます。

**[アプリ名]** フィールドは、バンドル ID の識別を容易にするわかりやすい名前を追加するために使われます。

### <a name="credential-renewal-certificate"></a>資格情報更新証明書

エンド ユーザーを (パスワードではなく) 証明書で認証する場合は、このフィールドを使って、認証証明書としてユーザーに展開される SCEP 証明書または PFX 証明書を選びます。 通常、これは VPN、WiFi、電子メールなどの他のプロファイル用にユーザーに展開されるものと同じ証明書です。

## <a name="next-steps"></a>次の手順

デバイスの機能の構成について詳しくは、「[Microsoft Intune でデバイスの機能設定を構成する方法](device-features-configure.md)」をご覧ください。