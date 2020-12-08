---
title: “关闭地址系列”概述
description: “关闭地址系列”概述
keywords:
- 地址系列 WDK 网络
- AFs WDK 网络
- 关闭地址系列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63fd71c3c77342965b40190dd16d8e5db19d7b7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817631"
---
# <a name="closing-an-address-family-overview"></a>“关闭地址系列”概述

面向连接的客户端调用 [**NdisClCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily) 删除其自身、呼叫管理器和特定基础 NIC 之间的关联。

如果 CoNDIS 独立调用管理器正在关闭到基础微型端口适配器的绑定，或微型 (MCM) 正在停止微型端口适配器，则调用管理器或 MCM 必须通知 NDIS，前提是应关闭关联的地址族 (AF) 。 然后，NDIS 通知每个 CoNDIS 客户端都打开了 AF，客户端应关闭 AF。

本节包括下列主题：

[关闭 CoNDIS 呼叫管理程序或 MCM](closing-a-condis-call-manager-or-mcm.md)

[关闭 CoNDIS 客户端中的地址系列](closing-an-address-family-in-a-condis-client.md)

 

