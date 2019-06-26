---
title: 默认 NDIS 端口
description: 默认 NDIS 端口
ms.assetid: a9edf83f-9226-4c75-a04e-1879a05df24c
keywords:
- WDK NDIS，默认端口
- NDIS 端口 WDK，默认 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17608f7871b4878163ddeb5653d625015ce77d30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354610"
---
# <a name="default-ndis-port"></a>默认 NDIS 端口





端口 0 保留为微型端口适配器的默认端口。 如果*PortNumber*的任何函数的参数或**PortNumber**任何结构的成员设置为零，而是微型端口驱动程序没有分配任何端口，或当前活动不是特定于端口的。

默认 NDIS 端口一个很好示例，请考虑负载平衡和故障转移 (LBFO) MUX 中间驱动程序。 此类驱动程序的虚拟微型端口可以是端口 0 （默认端口）。 中间驱动程序可以将端口为基础的微型端口适配器分配范围通过端口数为 1 的端口号 (*N*)。 基础驱动程序无法将数据发送到端口为零，则允许 LBFO 驱动程序，以选择其中一个基础的端口，或基础驱动程序可以指定介于 1 和端口号*N*选择发送操作的特定端口。

微型端口驱动程序无需分配任何端口，或者支持将默认端口以外的任何端口号。 即使微型端口驱动程序不会分配端口，NDIS 分配的默认端口，并将其激活后微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数设置注册中的属性[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。 微型端口驱动程序可以开始执行操作，在默认端口时**NdisMSetMiniportAttributes**成功返回。 在这种情况下，NDIS 释放的默认端口时微型端口驱动程序返回从[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数。

 

 





