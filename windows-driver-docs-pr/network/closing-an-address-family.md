---
title: 关闭地址族概述
description: 关闭地址族概述
ms.assetid: 0533bc31-dd4c-42c4-8170-8201e32e1026
keywords:
- 地址系列 WDK 网络
- AFs WDK 网络
- 关闭地址系列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e330313a40c2d5bab914227f0a6ee6a9ecc642b0
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565685"
---
# <a name="closing-an-address-family-overview"></a>关闭地址族概述

面向连接的客户端调用[**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)删除其自身、呼叫管理器和特定基础 NIC 之间的关联。

如果 CoNDIS 独立调用管理器正在关闭到基础微型端口适配器的绑定, 或微型端口调用管理器 (MCM) 正在停止微型端口适配器, 则调用管理器或 MCM 必须在关联的地址系列 (AF) 关闭时通知 NDIS。 然后, NDIS 通知每个 CoNDIS 客户端都打开了 AF, 客户端应关闭 AF。

本部分包括以下主题：

[关闭 CoNDIS 调用管理器或 MCM](closing-a-condis-call-manager-or-mcm.md)

[在 CoNDIS 客户端中关闭地址族](closing-an-address-family-in-a-condis-client.md)

 

 





