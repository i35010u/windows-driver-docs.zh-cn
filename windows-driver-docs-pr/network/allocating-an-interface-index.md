---
title: 分配接口索引
description: 分配接口索引
ms.assetid: f1315da2-16da-4320-9d0d-1270396af38b
keywords:
- NDIS 网络接口 WDK，接口索引分配
- 网络接口 WDK，接口索引分配
- 接口索引 WDK 网络
- 分配网络接口索引
- 索引操作 WDK 网络接口
- WDK 的本地唯一标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31446074b97bfda64a064564d7447249af36dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367803"
---
# <a name="allocating-an-interface-index"></a>分配接口索引





如果接口提供程序已成功注册了一个接口通过调用[ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)函数，NDIS 分配为该接口的接口索引，并返回位置的索引值位置的*pIfIndex*参数指定。 接口索引是本地计算机唯一一个 16 位值。 NDIS 不保证它将分配相同的接口索引，当接口提供程序注册相同[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)计算机重新启动后的值。 接口索引值为零 (NET\_IFINDEX\_未指定) 被保留，NDIS 不将其分配给任何接口。

 

 





