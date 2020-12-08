---
title: “启动和暂停微型端口适配器”概述
description: “启动和暂停微型端口适配器”概述
keywords:
- 微型端口适配器 WDK 网络，开始
- 适配器 WDK 网络，开始
- 微型端口适配器 WDK 网络，暂停
- 适配器 WDK 网络，暂停
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd21e2aa872b033756ac2e28baea1b12a82f70ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790421"
---
# <a name="starting-and-pausing-a-miniport-adapter-overview"></a>“启动和暂停微型端口适配器”概述





NDIS 暂停适配器以停止可能干扰即插即用操作的数据流，如添加或删除筛选器驱动程序或请求，如在 NIC 上设置数据包筛选器或多播地址列表。 有关如何修改正在运行的驱动程序堆栈的详细信息，请参阅 [修改正在运行的驱动程序堆栈](modifying-a-running-driver-stack.md)。

NDIS 将适配器从暂停状态重启。 适配器初始化完成后或暂停操作完成后，适配器将进入暂停的启动。

以下主题提供了有关启动和暂停以及适配器的详细信息：

-   [启动适配器](starting-an-adapter.md)
-   [暂停适配器](pausing-an-adapter.md)

 

 





