---
title: MacOS デバイスを消去する
titleSuffix: Microsoft Intune
description: macOS デバイスからオペレーティング システムを含むすべてのデータを消去する方法を説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/31/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 64f8b31c4fab5b247ae466df52a0b965f1be813b
ms.sourcegitcommit: 51b763e131917fccd255c346286fa515fcee33f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2018
ms.locfileid: "52179968"
---
# <a name="erase-all-data-from-a-macos-device"></a>MacOS デバイスからすべてのデータを消去する

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

macOS デバイスから、オペレーティング システムを含むすべてのデータを消去することができます。 デバイスは Intune の管理からも削除されます。 エンド ユーザーに警告は表示されません。

1. [Azure Portal の Intune](https://aka.ms/intuneportal) で、**[デバイス]** > **[すべてのデバイス]** の順に選び、消去するデバイスを選びます。
![スクリーンショット](./media/device-erase/choosedevice.png)
2. **[その他]** > **[消去]** の順にクリックし、**[Recovery Pin]\(回復用 PIN\)** に 6 桁の数字を入力します。 これは、ユーザーが自分のデバイスにオペレーティング システムを再インストールできるようにユーザーに与える必要がある PIN です。 この PIN は、消去操作が完了した後では表示できないので、必ず書き留めておいてください。
![スクリーンショット](./media/device-erase/providepin.png)
3. **[OK]** をクリックしてデバイスを消去します。
