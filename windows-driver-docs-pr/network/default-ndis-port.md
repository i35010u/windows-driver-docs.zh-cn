---
title: 默认 NDIS 端口
description: 默认 NDIS 端口
ms.assetid: a9edf83f-9226-4c75-a04e-1879a05df24c
keywords:
- WDK NDIS，默认端口
- NDIS 端口 WDK，默认 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcee3e9181e21c4d35bf18ae457016cfc4a5e0ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367669"
---
# <a name="default-ndis-port"></a>默认 NDIS 端口





端口 0 保留为微型端口适配器的默认端口。 如果*PortNumber*的任何函数的参数或**PortNumber**任何结构的成员设置为零，而是微型端口驱动程序没有分配任何端口，或当前活动不是特定于端口的。

默认 NDIS 端口一个很好示例，请考虑负载平衡和故障转移 (LBFO) MUX 中间驱动程序。 此类驱动程序的虚拟微型端口可以是端口 0 （默认端口）。 中间驱动程序可以将端口为基础的微型端口适配器分配范围通过端口数为 1 的端口号 (*N*)。 基础驱动程序无法将数据发送到端口为零，则允许 LBFO 驱动程序，以选择其中一个基础的端口，或基础驱动程序可以指定介于 1 和端口号*N*选择发送操作的特定端口。

微型端口驱动程序无需分配任何端口，或者支持将默认端口以外的任何端口号。 即使微型端口驱动程序不会分配端口，NDIS 分配的默认端口，并将其激活后微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数设置注册中的属性[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 微型端口驱动程序可以开始执行操作，在默认端口时**NdisMSetMiniportAttributes**成功返回。 在这种情况下，NDIS 释放的默认端口时微型端口驱动程序返回从[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。

 

 





