---
title: Better Mobile と Intune の統合を設定する
titleSuffix: Intune on Azure
description: Better Mobile コネクタと Intune の統合
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.openlocfilehash: 761605a74e6aeda65d9c6361b18b51e255873ac1
ms.sourcegitcommit: bee072b61cf8a1b8ad8d736b5f5aa9bc526e07ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53816533"
---
# <a name="integrate-better-mobile-with-intune"></a>Better Mobile と Intune を統合する

Better Mobile Threat Defense ソリューションを Intune と統合するには、次の手順を行います。

## <a name="before-you-begin"></a>始める前に

> [!NOTE]
> 次の手順は、[Better Mobile の管理コンソール](https://aad.bmobi.net)で完了する必要があります。

Better Mobile と Intune の統合を始める前に、次のものがあることを確認します。

-   Microsoft Intune サブスクリプション

-   次のアクセス許可を付与する Azure Active Directory 管理者資格情報:

    -   サインインしてユーザー プロファイルを読み取る

    -   サインインしたユーザーとしてディレクトリにアクセスする

    -   ディレクトリ データの読み込み

    -   Intune にデバイス情報を送信する

-   Better Mobile 管理コンソールにアクセスするための管理者資格情報。

### <a name="better-mobile-app-authorization"></a>Better Mobile アプリの承認

Better Mobile アプリの承認プロセスは以下で構成されます。

-   Better Mobile サービスがデバイスの正常性状態に関する情報を Intune に通知できるようにします。

-   Better Mobile は、Azure AD 登録グループ メンバーシップと同期してデバイスのデータベースを設定します。

-   Better Mobile 管理コンソールが Azure AD シングル サインオン (SSO) を使用できるようにします。

-   Better Mobile アプリが Azure AD SSO を使用してサインインできるようにします。

## <a name="to-set-up-better-mobile-integration"></a>Better Mobile の統合を設定するには

1. [Better Mobile の管理コンソール](https://aad.bmobi.net)に移動し、資格情報を使用してサインインします。
2. **[統合]** > **[EMM/MDM]** > **[アカウントの追加]** の順に選択します。

     ![Better Mobile の管理コンソールの画像](media/better_mobile_console.png)
 
3. **[Intune]** を選択します。
4. **[アカウント名]** の横に、記述子を入力します。 
5. **Microsoft のサインイン**のウィンドウに Intune の資格情報を入力します。
6. **[要求されているアクセス許可]** ウィンドウで、**[Accept]\(同意\)** を選択します。
7. Better Mobile を同期するデバイスが属する Azure AD セキュリティ グループを検索し、一覧から選択します。 **[続行]** を選択します。
8. **[完了]** を選びます。
9. **[アカウントの追加]** ページが再表示されます。 ページを閉じます。 

## <a name="next-steps"></a>次の手順

-   [Better Client アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)