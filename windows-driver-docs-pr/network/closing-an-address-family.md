---
title: 关闭地址系列
description: 关闭地址系列
ms.assetid: 0533bc31-dd4c-42c4-8170-8201e32e1026
keywords:
- 地址系列 WDK 网络
- AFs WDK 网络
- 关闭地址系列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6338ada64df707970e8770ada8567d875680b88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356932"
---
# <a name="closing-an-address-family"></a>关闭地址系列





在面向连接的客户端调用[ **NdisClCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561626)删除本身、 调用管理器中与特定的基础 NIC 之间的关联

当 CoNDIS 独立调用管理器正在关闭一个绑定到基础的微型端口适配器或微型端口调用管理器 (MCM) 导致停止的微型端口适配器时，呼叫管理器或 MCM 如果应将其关闭关联的地址族 (AF)，则必须通知 NDIS。 然后，NDIS 会通知已打开 AF 每个的 CoNDIS 客户端在客户端应关闭 AF。

本部分包括以下主题：

[关闭的 CoNDIS 呼叫管理器或 MCM](closing-a-condis-call-manager-or-mcm.md)

[关闭的 CoNDIS 客户端中的地址族](closing-an-address-family-in-a-condis-client.md)

 

 





