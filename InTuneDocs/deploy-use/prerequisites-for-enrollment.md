---
title: "モバイル デバイスの登録の前提条件 | Microsoft Intune"
description: "モバイル デバイス管理 (MDM) の前提条件の設定、およびさまざまなオペレーティング システムに登録する準備。"
keywords: 
author: staciebarker
ms.author: stabar
manager: angrobe
ms.date: 07/25/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 44fd4af0-f9b0-493a-b590-7825139d9d40
ms.reviewer: damionw
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c59707ba2967b069dc30aee71d2642e91d71b23b
ms.openlocfilehash: 270e6015e629c048b01b218793640888706d118e


---

# <a name="prerequisites-for-mobile-device-management-in-intune"></a>Intune でのモバイル デバイス管理の前提条件
従業員が自分のモバイル デバイスを Intune に登録できるようにするには、以下の手順に従う必要があります。 会社所有のデバイスを管理する場合も同じ手順が必要です。

|手順|説明|  
|-----------|-------------|  
|**手順 1:** [接続を有効にする](#step-1-enable-connections)|カスタム ドメイン名が構成されていて、ネットワーク通信の準備が整っていることを確認します。|  
|**手順 2:** [MDM 機関を設定する](#step-2-set-mdm-authority)|モバイル デバイス管理機関は、お客様のデバイスに割り当てるサービスを定義します。|
|**手順3:** [グループを作成する](#step-3-create-groups)|ユーザーの要求に応じてポータル サイト アプリの設定を構成します。|  
|**手順 4:** [ポータル サイトを構成する](#step-4-configure-company-portal)|ユーザーの要求に応じてポータル サイト アプリの設定を構成します。|  
|**手順 5:** [ユーザー ライセンスを割り当てる](#step-5-assign-user-licenses)|ユーザーがデバイスを登録できるようにユーザーに Intune ライセンスを割り当てます。|
|**手順 6:** [登録を有効にする](#step-6-enable-enrollment)|iOS および Windows での管理に備えてプラットフォームに固有の設定を有効にします。 Android デバイスでは、追加の構成は不要です。|
|**手順 7:** [次のステップ](#step-7-next-steps)|iOS および Windows での管理に備えてプラットフォームに固有の設定を有効にします。 Android デバイスでは、追加の構成は不要です。|

Configuration Manager で Intune を管理するには
> [!div class="button"]
[SCCM のドキュメントを見る >](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm)

## <a name="step-1-enable-connections"></a>手順 1: 接続を有効にする

モバイル デバイスの登録を有効にする前に、次のことが完了していることを確認してください。
- [必要なネットワーク URL とポートの確認](../get-started/network-infrastructure-requirements-for-microsoft-intune.md)
- [ドメイン名の追加と検証](../get-started/domain-names-for-microsoft-intune.md)

## <a name="step-2-set-mdm-authority"></a>手順 2: MDM 機関を設定する
MDM 機関では、一連のデバイスを管理するためのアクセス許可を持つ管理サービスを定義します。 MDM 機関のオプションには、Intune 単体で使用するか、Intune を Configuration Manager と連携させて使用する方法があります。 Configuration Manager を管理機関として設定した場合、モバイル デバイス管理のために使用できるサービスは他にありません。

>[!IMPORTANT]
> モバイル デバイスの管理に Intune のみ (オンライン サービス) を使用するか、System Center Configuration Manager と Intune との統合 (オンプレミス ソフトウェア ソリューションをオンライン サービスと組み合わせて使用) を使用するのかについて、慎重に検討します。 モバイル デバイス管理機関は、設定後に変更することはできません。



1.  [Microsoft Intune 管理コンソール](http://manage.microsoft.com)で、**[管理]** &gt; **[モバイル デバイス管理]** の順に選択します。

2.  **[タスク]** リストで **[モバイル デバイス管理機関の設定]**をクリックします。 **[MDM 機関の設定]** ダイアログ ボックスが開きます。

    ![[MDM 機関の設定] ダイアログ ボックス](../media/intune-mdm-authority.png)

3.  Intune によって、Intune を MDM 機関にすることを確認するよう求められます。 チェック ボックスを選択してから、**[はい]** を選択し、Microsoft Intune を使用してモバイル デバイスを管理します。

## <a name="step-3-create-groups"></a>手順3: グループを作成する

ユーザー グループとデバイス グループを作成して、管理を簡略化し、展開されるアプリ、ポリシー、会社のリソースのターゲット設定を向上できます。 [グループを作成する方法についての説明](use-groups-to-manage-users-and-devices-with-microsoft-intune.md#create-groups)を参照してください。

## <a name="step-4-configure-company-portal"></a>手順 4: ポータル サイトを構成する

ユーザーは、Intune ポータル サイトを使用して、会社のデータにアクセスしたり、デバイスの登録、アプリケーションのインストール、IT 部門からのサポート情報の検索などの一般的なタスクを実行したりできます。

> [!TIP]
> ポータル サイトをカスタマイズすると、構成がポータル サイトの Web サイトとポータル サイト アプリの両方に適用されます。

ポータル サイトをカスタマイズすることで、エンド ユーザーの利便性を向上させることができます。 これを行うには、テナント管理者またはサービス管理者として [Microsoft Intune 管理コンソール](https://manage.microsoft.com)にサインインし、**[管理者]** &gt; **[ポータル サイト]** の順にクリックして、ポータル サイトの設定を構成します。

![admin-console-admin-workspace-comp-portal-settings](../media/cp_sa_cpsetup.PNG)

### <a name="company-contact-information-and-privacy-statement"></a>会社の連絡先情報とプライバシーに関する声明

会社名は、ポータル サイトのタイトルとして表示されます。 連絡先情報と詳細は、ポータル サイトの [IT に連絡] 画面でユーザーに対して表示されます。 プライバシーに関する声明は、ユーザーがプライバシー リンクをクリックすると表示されます。

|フィールド名|最大長|詳細情報|
    |----------|------------------------|----------------|
    |会社名|40|ポータル サイトのタイトルとして表示される名前です。 **注**: 英数字のみです。 このフィールドでは特殊文字を使用できません。|
    |IT 部門の担当者名|40|**[IT に連絡]** ページに表示される名前です。|
    |IT 部門の電話番号|20|**[IT に連絡]** ページに表示される連絡先の電話番号です。|
    |IT 部門の電子メール アドレス|40|**[IT に連絡]** ページに表示される連絡先の電子メール アドレスです。 **alias@domainname.com** の形式で有効な電子メール アドレスを入力する必要があります。|
    |追加情報|120|[IT に連絡]** ページに表示される情報です。|
    |会社のプライバシーに関する声明の URL|79|ポータル サイトでユーザーがプライバシー リンクをクリックすると表示される、各社のプライバシーに関する声明を指定できます。 https://www.contoso.com の形式で URL を入力します。|

### <a name="support-contacts"></a>サポートの連絡先
サポート Web サイトは、ポータル サイトに表示されます。ユーザーは、サポート サイトからオンライン サポートを利用できます。

|フィールド名|最大長|詳細情報|
    |----------|------------------------|----------------|
    |サポート Web サイトの URL|150|ユーザーが使用するサポート Web サイトがある場合、その URL を指定します。 URL は、https://www.contoso.com という形式にする必要があります。 URL を指定しない場合、ポータル サイトの **[IT に連絡]** ページのサポート Web サイトには何も表示されません。|
    |Web サイト名|40|サポート Web サイトの URL に表示されるフレンドリ名です。 サポート Web サイトの URL を指定し、フレンドリ名を指定しない場合、ポータル サイトの **[IT に連絡]** ページに **[IT Web サイトに移動する]** が表示されます。|


### <a name="company-branding-customization"></a>会社のブランドのカスタマイズ

ポータル サイトのロゴや会社名、テーマの色や背景をカスタマイズできます。

|フィールド名|詳細情報|
    |----------|----------------|
    |テーマの色|ポータル サイトに適用するテーマの色を選択します。|
    |会社のロゴを含める|このオプションを有効にすると、ポータル サイトに表示する会社のロゴをアップロードできます。 2 つのロゴをアップロードできます。1 つは、ポータル サイトの背景が白の場合に表示するロゴ、もう 1 つは、選択したテーマの色がポータル サイトの背景に使用されている場合に表示するロゴです。 各ロゴは、.png または .jpg ファイルにし、最大解像度が 400 x 100 ピクセルで、750 KB 以下のサイズにします。|
    |ポータル サイト アプリ用の背景を選択する|この設定は、ポータル サイト アプリの背景のみに適用されます。|


変更を保存した後で、管理コンソールの **[ポータル サイト]** ページの下部に表示されるリンクを使用して、ポータル サイト Web サイトを表示できます。 これらのリンクは変更できません。 ユーザーがサインインするときに、これらのリンクでポータル サイトが表示されます。

## <a name="step-5-assign-user-licenses"></a>手順 5: ユーザー ライセンスを割り当てる

**Office 365 管理ポータル**を使用して、手動でクラウドベースのユーザーを追加し、クラウドベースのユーザー アカウントと、オンプレミスの Active Directory から Azure Active Directory (Azure AD) に同期されているアカウントの両方にライセンスを割り当てます。 [オンプレミスのユーザーを Azure AD と同期する](../get-started/start-with-a-paid-subscription-to-microsoft-intune-step-3.md#how-to-sync-on-premises-users-with-azure-ad)ことができます。

1.  テナント管理者の資格情報を使用して、[Office 365 管理ポータル](https://portal.office.com/Admin/Default.aspx)にサインインします。

2.  Intune のユーザー ライセンスを割り当てるユーザー アカウントを選択し、そのユーザー アカウントのプロパティの **[Microsoft Intune]** チェック ボックスを選択します。

3.  これで、ユーザー アカウントが Microsoft Intune ユーザー グループに追加され、サービスを使用し、デバイスを管理対象に登録する権限がユーザーに付与されます。

### <a name="to-synchronize-on-premises-users-with-azure-ad"></a>オンプレミスのユーザーを Azure AD と同期するには

1. オンプレミス Active Directory でカスタム ドメインの [UPN サフィックスを追加します](https://technet.microsoft.com/en-us/library/cc772007.aspx)。
2. インポートする予定のオンプレミス ユーザー用に新しい UPN サフィックスを設定します。
3. [Azure AD Connect Sync](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect/) を実行して、オンプレミス ユーザーを Azure AD と統合します。
4. ユーザー アカウント情報が正常に同期したら、[Office 365 管理ポータル](https://portal.office.com/Admin/Default.aspx)を使用して Microsoft Intune ライセンスを割り当てることができます。

## <a name="step-6-enable-enrollment"></a>手順 6: 登録を有効にする
MDM 機関を設定したら、組織がサポートするオペレーティング システムにデバイス管理をセットアップする必要があります。 デバイス管理のセットアップに必要な手順は、オペレーティング システムによって異なります。 たとえば、Android OS では、Intune 管理コンソールで必要になる操作はありません。 これに対して、Windows および iOS では管理を許可するため、デバイスと Intune との間に信頼関係が必要です。

次のプラットフォームの管理を設定します。
- [iOS および Mac >](set-up-ios-and-mac-management-with-microsoft-intune.md)
- [Android](set-up-android-management-with-microsoft-intune.md)
- [Android for Work](set-up-android-for-work.md)
- [Windows PC とノート PC](set-up-windows-device-management-with-microsoft-intune.md)
- [Windows 10 Mobile と Windows Phone](set-up-windows-phone-management-with-microsoft-intune.md)

[企業所有デバイスの登録](manage-corporate-owned-devices.md)を有効にすることもできます。

## <a name="step-7-next-steps"></a>手順 7: 次のステップ

登録が有効になったので、ビジネス ニーズを満たす管理を設定する必要があります。 一部の管理オプションを次に示します。

- [デバイスの設定と機能を管理するポリシーを展開する](manage-settings-and-features-on-your-devices-with-microsoft-intune-policies.md)
- [電子メール、Wi-Fi、VPN などの会社のリソースへのアクセスを有効にする](enable-access-to-company-resources-with-microsoft-intune.md)
- [アプリを追加](add-apps.md)し、管理対象デバイスに[アプリを展開](deploy-apps.md)する
- [デバイス コンプライアンス ポリシーを作成](introduction-to-device-compliance-policies-in-microsoft-intune.md)し、[コンプライアンスに基づいてアクセスを制限](restrict-access-to-email-and-o365-services-with-microsoft-intune.md)する



<!--HONumber=Dec16_HO2-->

