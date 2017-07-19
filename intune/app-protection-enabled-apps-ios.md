---
title: "アプリ保護ポリシーのある iOS アプリ"
titleSuffix: Intune on Azure
description: "このトピックでは、アプリ保護ポリシーを使用して iOS アプリを管理するときの注意点について説明します。\""
keywords: 
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 586d9440-3813-4dec-b865-8bd319befde0
ms.reviewer: andcerat
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 912bc5230904f5798b2e0026dcf0dd1cecdb811c
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2017
---
<a id="what-to-expect-when-your-ios-app-is-managed-by-app-protection-policies" class="xliff"></a>

# アプリ保護ポリシーを使用して iOS アプリを管理するときの注意点
[!INCLUDE[azure_portal](./includes/azure_portal.md)] このトピックでは、アプリ保護ポリシーを使用する場合のアプリのユーザー エクスペリエンスについて説明します。 アプリ保護ポリシーが適用されるのは、作業アカウントを使用してアプリにアクセスしたり、会社の OneDrive 事業拠点に格納されたファイルにアクセスしたりするなどのワーク コンテキストでアプリが使用される場合に限定されます。
<a id="accessing-apps" class="xliff"></a>

##  アプリへのアクセス

デバイスが**Intune に登録されていない**場合、エンドユーザーはアプリを初めて使用すると、アプリの再起動を求められます。  再起動すると、アプリ保護ポリシーをアプリに適用することができます。 次のスクリーンショットは、Skype アプリを使用した場合の例を示しています。


![暗証番号 (PIN) を求めるプロンプトを表示している iOS のスクリーン ショット](./media/ios-pin-prompt.png)

**Intune の管理対象として登録された**デバイスの場合、エンドユーザーにはアプリが管理された状態にあることを示すメッセージが表示されます。

![会社によって管理された状態にあることを示すメッセージと、暗証番号 (PIN) を求めるプロンプトが表示されている iOS デバイスのスクリーンショット](./media/ios-managed-devices-pin-prompt.png)

<a id="using-apps-with-multi-identity-support" class="xliff"></a>

##  複数の ID を使用するアプリのサポート

アプリ保護ポリシーはアプリがワーク コンテキストで使用されている場合にのみ適用されます。そのため、ワーク コンテキストとパーソナル コンテキストでは、アプリの動作に違いが見られることがあります。  

複数の ID をサポートするアプリに対しては、Intune は、エンドユーザーがアプリをワーク コンテキストで使用している場合にのみアプリ保護ポリシーを適用します。  たとえば、エンドユーザーが職場のデータにアクセスすると、暗証番号 (PIN) を求めるプロンプトが表示されます。  **Outlook アプリ** の場合、エンドユーザーにはアプリの起動時に、暗証番号 (PIN) の入力を求めるプロンプトが表示されます。 **OneDrive アプリ** の場合は、エンドユーザーが作業アカウントを入力すると、同様のプロンプトが表示されます。  Microsoft **Word**、**PowerPoint*、**Excel** の場合は、エンドユーザーが会社の OneDrive for Business 拠点に保存されたドキュメントにアクセスすると、同様のプロンプトが表示されます。
<a id="managing-user-accounts-on-the-device" class="xliff"></a>

##  デバイスのユーザー アカウントの管理

Intune では、アプリ保護ポリシーをデバイスごとに 1 つのユーザー アカウントのみに展開することがサポートされます。

* 2 つ目のユーザーがデバイスでブロックされるかどうかは、使用中のアプリによって決まります。 ただし、どの場合でも、ポリシーの影響を受けるのは、アプリ保護ポリシーが適用される最初のユーザーのみです。
  * **Microsoft Word**、**Excel**、**PowerPoint** では、2 つ目のユーザー アカウントがブロックされることはありませんが、2 つ目のユーザー アカウントがアプリ保護ポリシーの影響を受けることはありません。  

  * **OneDrive アプリと Outlook アプリ**では、作業アカウントは 1 つだけ使用できます。  作業アカウントを複数追加しようとしても、これらのアプリでブロックされます。  ただし、デバイス上のユーザーを削除して、別のユーザーを追加することはできます。

* アプリ保護ポリシーを展開する前にデバイスに複数の既存のユーザー アカウントがある場合は、アプリ保護ポリシーが展開される最初のアカウントが Intune アプリ保護ポリシーによって管理されます。


次のサンプル シナリオを読んで、複数のユーザー アカウントがどのように処理されるかを深く理解してください。

ユーザー A は、**会社 X** と会社 **会社 Y** という 2 つの会社で働いています。ユーザー A は各会社の作業アカウントを持っており、どちらの会社も Intune を使用してアプリ保護ポリシーを展開しています。 **会社 X** は、**会社 Y** の**前に**アプリ保護ポリシーを展開しています。アプリ保護ポリシーは、**会社 X** に関連付けられたアカウントに適用され、会社 Y に関連付けられたアカウントには適用されません。会社 Y に関連付けられたユーザー アカウントをアプリ保護ポリシーで管理する場合は、会社 X に関連付けられたユーザー アカウントを削除する必要があります。
<a id="adding-a-second-account" class="xliff"></a>

### 2 つ目のアカウントの追加

iOS デバイスを使用している場合は、同じデバイスに 2 つ目の作業アカウントを追加しようとすると、ブロック メッセージが表示されることがあります。  アカウントが表示され、削除するアカウントを選択できるようになります。

![ブロック メッセージと、[はい] と [いいえ] オプショを表示しているダイアログ ボックスのスクリーンショット](./media/ios-switch-user.PNG)

<a id="next-steps" class="xliff"></a>

## 次のステップ
[アプリ保護ポリシーを使用して Android アプリを管理するときの注意点](app-protection-enabled-apps-android.md)
<a id="see-also" class="xliff"></a>

### 関連項目
[Microsoft Intune でのアプリ保護ポリシーの作成と展開](app-protection-policies.md)