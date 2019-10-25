---
title: 默认 NDIS 端口
description: 默认 NDIS 端口
ms.assetid: a9edf83f-9226-4c75-a04e-1879a05df24c
keywords:
- 端口 WDK NDIS，默认值
- NDIS 端口 WDK，默认 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa9056de179be320963a3f57436bed4c72f7d741
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838172"
---
# <a name="default-ndis-port"></a>默认 NDIS 端口





端口0保留为微型端口适配器的默认端口。 如果任何函数的*PortNumber*参数或任何结构的**PortNumber**成员均设置为零，则表示小型端口驱动程序未分配任何端口，或者当前活动不是特定于端口的。

如需默认 NDIS 端口的典型示例，请考虑使用负载平衡和故障转移（LBFO） MUX 中间驱动程序。 此类驱动程序的虚拟微型端口可以是端口零（默认端口）。 中间驱动程序可以使用端口号（范围从1到端口数（*N*））将端口分配给基础微型端口适配器。 过量驱动程序可以将数据发送到端口零，以允许 LBFO 驱动程序选择某个基础端口，或者过量驱动程序可以指定从1到*N*的端口号，以便为发送操作选择特定端口。

微型端口驱动程序无需分配任何端口或支持除默认端口以外的任何端口号。 即使微型端口驱动程序未分配端口，NDIS 也会分配默认端口，并在微型端口驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数以在[**NDIS\_微型端口中设置注册属性后激活它\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。 当**NdisMSetMiniportAttributes**成功返回时，微型端口驱动程序可以对默认端口启动操作。 在这种情况下，当微型端口驱动程序从[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数返回时，NDIS 将释放默认端口。

 

 





