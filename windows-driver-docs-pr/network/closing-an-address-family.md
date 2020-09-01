---
title: “关闭地址系列”概述
description: “关闭地址系列”概述
ms.assetid: 0533bc31-dd4c-42c4-8170-8201e32e1026
keywords:
- 地址系列 WDK 网络
- AFs WDK 网络
- 关闭地址系列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4c8ac10f9eb3a651b9d819fff2fd567110ad53
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218119"
---
# <a name="closing-an-address-family-overview"></a>“关闭地址系列”概述

面向连接的客户端调用 [**NdisClCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily) 删除其自身、呼叫管理器和特定基础 NIC 之间的关联。

如果 CoNDIS 独立调用管理器正在关闭到基础微型端口适配器的绑定，或微型 (MCM) 正在停止微型端口适配器，则调用管理器或 MCM 必须通知 NDIS，前提是应关闭关联的地址族 (AF) 。 然后，NDIS 通知每个 CoNDIS 客户端都打开了 AF，客户端应关闭 AF。

本节包括下列主题：

[关闭 CoNDIS 呼叫管理程序或 MCM](closing-a-condis-call-manager-or-mcm.md)

[关闭 CoNDIS 客户端中的地址系列](closing-an-address-family-in-a-condis-client.md)

 

