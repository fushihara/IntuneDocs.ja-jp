---
title: "デバイスに証明書がない | Microsoft Docs"
description: 
keywords: 
author: barlanmsft
ms.author: barlan
manager: angrobe
ms.date: 01/04/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: f0ba4cbb-ef0a-4335-86bf-f1d006867fa2
searchScope:
- Company Portal
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: arnab
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6fcfac7c8bd469f5163ec9b4017ae8c3d486428
ms.openlocfilehash: 88770ba06718a767f8229e1b5aa4d543c87bc852

---

# <a name="your-android-device-is-missing-a-certificate-required-by-your-it-admin"></a>Android デバイスに、IT 管理者が必要とする証明書がありません

デバイスが Intune に登録されておらず、IT 管理者が必要とする特定の証明書がない場合は、ポータル サイト アプリにサインインすることはできません。 サインインしようとすると、次のメッセージが表示されます。

![screenshot-error-message-about-missing-certificate](./media/andr-cert_install-1-cert_missing.png)

この問題を解決し、必要な証明書を取得するために、次の 2 つの主な手順を行う必要があります。

- 会社または学校の PC を確認し、欠落している証明書を特定します。
- デバイスを使用して、欠落している証明書をインターネットからダウンロードします。

## <a name="identify-the-missing-certificate-by-looking-on-a-company-or-school-pc"></a>欠落している証明書を会社または学校の PC で確認し、特定する

1. PC で、Internet Explorer を開きます。 この目的に使用する PC をお持ちでない場合は、IT 管理者に問い合わせてください。 管理者の連絡先情報については、[ポータル サイト Web サイト](http://portal.manage.microsoft.com)をご確認ください。

2. [ポータル サイト Web サイト](http://portal.manage.microsoft.com)に移動して、職場や学校の資格情報を使用してサインインします。

3. ブラウザーのアドレス バーの右端で、下のスクリーンショットのような、南京錠のような記号をクリックします。

    ![screenshot-internet-explorer-address-bar-padlock-symbol](./media/andr-missing-cert-ie-padlock-symbol.png)

    南京錠の記号が表示されない場合は作業を停止し、IT 管理者に問い合わせてください。 このロックは、安全にサインインされていることを意味するため、その記号が表示されるまで作業を続行しないでください。

4. **[View certificates]** (証明書の表示) を選択します。

    ![screenshot-internet-explorer-view-certificates-button-on-website-identification-dialog](./media/andr-missg-cert-ie-view-cert-button.png)

5. **[証明書]** ダイアログ ボックスで **[Certification path]** (証明パス) タブを選択し、インターネットから取得する必要がある証明書を特定します。 必要な証明書の名前は、上記の例のスクリーン ショットで強調表示されている場所と同じ位置にあります。

## <a name="download-and-install-the-missing-certificate-on-your-android-mobile-device"></a>Android モバイル デバイスで欠落している証明書をダウンロードしてインストールする

1. Bing や Google のような検索エンジンを使用して、前のセクションで特定した、欠落している証明書の名前を検索します。 証明書の「拡張子」は、それぞれ ".crt" または ".pem" などのように異なる可能性があります。

2. ルート証明書を Web サイトからダウンロードします。

3. 証明書をダウンロードした後、デバイスの上部から下にドラッグして通知を開き、通知の一覧にある証明書の名前をタップします。

4. 次のスクリーンショットのような **[Name the Certificate]** (証明書の名前指定) ダイアログ ボックスで、既定の証明書名を受け入れます。

5. **[認証情報の使用]** が **[VPN とアプリ]** に設定されていることを確認し、**[OK]** をタップします。

    ![screenshot-certificate-name-dialog-showing-certificate-name](./media/andr-missing-cert-cert-name.png)

6. 会社のポータル アプリを閉じます。

7. 会社のポータル アプリをもう一度開きます。 これで、会社のポータル アプリにサインインできるようになりました。 サポートが必要な場合は、IT 管理者に問い合わせてください。

上のような "証明書が見つかりません" というメッセージが表示されたが、この手順を既に実行している場合、別の証明書が存在する可能性があります。IT 管理者にそのインストールを依頼する必要があります。 サポートを得るには、[ポータル Web サイト](http://portal.manage.microsoft.com)で入手できる連絡先情報を使用して IT 管理者に問い合わせてください。



<!--HONumber=Jan17_HO1-->

