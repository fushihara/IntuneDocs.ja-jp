---
title: Microsoft Intune で Exchange の条件付きアクセスを監視する | Microsoft Intune
description: Intune Azure ポータルを使用し、Exchange On-Premises と Exchange Online の条件付きアクセス コンプライアンスを監視します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/22/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 5712682d-285b-43fd-9978-3dcfd95ec5f9
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 8c9602dbe183501cc779fcb9b5d5a1e6e4bf6154
ms.sourcegitcommit: bee072b61cf8a1b8ad8d736b5f5aa9bc526e07ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53816772"
---
# <a name="monitor-conditional-access-compliance-for-on-premises-exchange-and-exchange-online-in-intune"></a>Intune で Exchange On-Premises および Exchange Online の条件付きアクセス コンプライアンスを監視する

Intune 1704 リリース以降では、管理者は、内部設置型 Exchange Connector またはサービス間コネクタ (Exchange Online Connector) を使って、Intune と同期化される Exchange ActiveSync デバイス レコードに関するレポート情報を見ることができます。 条件付きアクセス コンプライアンス レポートでは、さまざまな同期状態のデバイスの概要が提供されます。

-   **許可**

-   **ブロック**

-   **検疫**

## <a name="to-monitor-conditional-access-compliance"></a>条件付きアクセス コンプライアンスを監視するには

1.  [Azure Portal](https://portal.azure.com/) に移動し、Intune 資格情報でサインインします。

2.  正常にサインインすると、**Azure ダッシュボード**が開きます。

3.  左側のメニューから **[すべてのサービス]** を選択し、テキスト ボックス フィルターに「 **Intune** 」と入力します。

4.   **[Intune]** を選ぶと、 **Intune ダッシュボード** が表示されます。

5.  **[条件付きアクセス]** を選択し、**[概要]** を選択します。

6.  チャートの 3 つの領域 (**[許可]**、**[ブロック済み]**、 **[検疫]**) のいずれかを選択し、条件付きアクセス コンプライアンス レポートを表示します。

    ![条件付きアクセス ダッシュボードの画像](./media/CA-reporting-intune-1.png)

3 つの領域のいずれかを選択すると、許可、ブロック、または検疫されているデバイスについての詳細を確認できます。

特定のデバイスにドリルダウンしてさらに詳細な情報を見ることもできます。 たとえば、次の画像で選択されているデバイスはブロックされています。 Intune では、条件付きアクセス コンプライアンス レポート ウィンドウから企業データを削除できます。

![条件付きアクセス デバイス詳細レポートの画像](./media/CA-reporting-intune-3.png)

デバイスの詳細ウィンドウでは、さらに情報を表示できます。

-   **[概要]:** 次のようなデバイスのプロパティを見ることができます。OS のバージョン、デバイス モデル、所有権、シリアル番号、デバイスの製造元、電話番号、デバイスの最終チェックイン日時など。

-   **プロパティ:** デバイスの所有権 (個人または企業) を設定できます。

-   **[ハードウェア]:**[概要] の情報に加えて、ストレージの詳細 (合計容量と空き容量)、システム エンクロージャ、ネットワークの詳細、ネットワーク サービス、およびその他の条件付きアクセスのブロックの詳細が表示されます。

-   **[検出されたアプリ]:** デバイスにインストールされているすべてのアプリケーションが表示されます。 インストールされているアプリの一覧を .CSV 形式にエクスポートすることもできます。

-   **[コンプライアンス]:** すべてのデバイス コンプライアンス ポリシーの詳細が表示されます。

-   **[デバイス構成]:** すべてのデバイス構成の詳細が表示されます。

-   **[Exchange へのアクセス]:** 条件付きアクセス ポリシーを適用した後のデバイスの状態についてさらに詳しく確認できます。
