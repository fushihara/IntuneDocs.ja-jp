---
title: "Intune 教育設定を構成する"
titleSuffix: Intune Azure preview
description: "Intune Azure プレビュー: Intune を使用して、管理対象デバイスの教育設定を構成する方法について説明します。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: ca4f1adc5704ecd66d2af7823f95ca63ec20469e
ms.openlocfilehash: 5c73719c4fd2805f91c6af3ba48c39f5d798aaeb
ms.lasthandoff: 03/17/2017


---

# <a name="how-to-configure-education-settings-in-microsoft-intune"></a>Microsoft Intune で教育設定を構成する方法

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

教育プロファイルには、Windows テスト アプリを構成する詳細 (アカウント詳細を含む) とテスト URL を指定できます。 これを構成するとき、テスト アプリが開き、指定したテストが表示されます。テストが完了するまで他のアプリはデバイスで実行できません。

このトピックでは、デバイスの制限プロファイルを構成する基本的な方法について説明します。その後、デバイスごとの詳細については、各プラットフォームのトピックを参照してください。

## <a name="create-a-device-profile-containing-education-profile-settings"></a>教育プロファイル設定を含むデバイス プロファイルの作成

1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[その他]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[デバイス構成]** を選択します。
2. **[デバイス構成]** ブレードで、**[管理]** > **[プロファイル]** の順に選択します。
3. [プロファイル] ブレードで、**[プロファイルを作成します]** を選択します。
4. **[プロファイルを作成します]** ブレードで、デバイスの制限プロファイルの**名前**と**説明**を入力します。
5. **[プラットフォーム]** ドロップダウン リストで、**[Windows 10 以降]** を選択します。
6. **[プロファイルの種類]** ドロップダウン リストで、**[教育プロファイル]** を選択します。 
7. [設定]、[構成] の順に選択し、**[テスト]** ブレードで次のように構成します。
    - **アカウント ユーザー名** - テストで使用するアカウントのユーザー名を入力します。 ユーザー名には、ドメイン アカウント、Azure Active Directory (AAD) アカウント、ローカルのコンピューター アカウントを指定できます。
    - **評価 URL** - ユーザーに受けさせるテストの URL を指定します。 詳細については、テストに関するドキュメントを参照してください。
    - **画面の監視** - ユーザーがテストを受けている間、画面の行動を監視できるかどうかを指定します。
    - **テキストの候補** - ユーザーがテストを受けている間、テキスト候補の表示を許可するか、禁止します。
8. 完了したら、**[プロファイルを作成します]** ブレードに戻り、**[作成]** をクリックします。

プロファイルが作成され、プロファイルの一覧ブレードに表示されます。
このプロファイルをグループに割り当てる場合は、[デバイス プロファイルを割り当てる方法](how-to-assign-device-profiles.md)に関する記事を参照してください。



