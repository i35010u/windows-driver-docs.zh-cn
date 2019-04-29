---
title: 启动和暂停微型端口适配器
description: 启动和暂停微型端口适配器
ms.assetid: d278b331-90d9-4d19-bf00-732981962522
keywords:
- 微型端口适配器 WDK 网络启动
- 适配器 WDK 网络启动
- 微型端口适配器 WDK 连接网络、 暂停
- 适配器 WDK 连接网络、 暂停
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7cc9ef56c74eb8644c19128be1503737d942f76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390632"
---
# <a name="starting-and-pausing-a-miniport-adapter"></a>启动和暂停微型端口适配器





NDIS 暂停适配器在数据流可能会干扰插操作，例如添加或删除筛选器驱动程序或请求，例如在 NIC 上设置的数据包筛选器或多播的地址列表 有关如何修改正在运行的驱动程序堆栈的详细信息，请参阅[修改运行驱动程序堆栈](modifying-a-running-driver-stack.md)。

NDIS 重新启动适配器从暂停状态。 适配器初始化完成后或暂停操作完成后，适配器将进入已暂停开始。

以下主题提供有关启动和暂停和适配器的详细信息：

-   [启动适配器](starting-an-adapter.md)
-   [暂停适配器](pausing-an-adapter.md)

 

 





