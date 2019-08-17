---
title: 启动和暂停微型端口适配器概述
description: 启动和暂停微型端口适配器概述
ms.assetid: d278b331-90d9-4d19-bf00-732981962522
keywords:
- 微型端口适配器 WDK 网络, 开始
- 适配器 WDK 网络, 开始
- 微型端口适配器 WDK 网络, 暂停
- 适配器 WDK 网络, 暂停
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46dbbb373a15d1defa6cab7341fcc18f5d55888e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565739"
---
# <a name="starting-and-pausing-a-miniport-adapter-overview"></a>启动和暂停微型端口适配器概述





NDIS 暂停适配器以停止可能干扰即插即用操作的数据流, 如添加或删除筛选器驱动程序或请求, 如在 NIC 上设置数据包筛选器或多播地址列表。 有关如何修改正在运行的驱动程序堆栈的详细信息, 请参阅[修改正在运行的驱动程序堆栈](modifying-a-running-driver-stack.md)。

NDIS 将适配器从暂停状态重启。 适配器初始化完成后或暂停操作完成后, 适配器将进入暂停的启动。

以下主题提供了有关启动和暂停以及适配器的详细信息:

-   [启动适配器](starting-an-adapter.md)
-   [暂停适配器](pausing-an-adapter.md)

 

 





