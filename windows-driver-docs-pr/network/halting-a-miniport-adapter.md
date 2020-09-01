---
title: 停止微型端口适配器
description: 停止微型端口适配器
ms.assetid: fd57a2b1-593d-412b-96b5-eabd3ea392e0
keywords:
- 微型端口适配器 WDK 网络，停止
- 适配器 WDK 网络，停止
- 暂停状态 WDK 网络
- MiniportHaltEx
- 停止适配器
- 正在停止适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b759c276efe5037d08902ac73e6820116f0bb39e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207303"
---
# <a name="halting-a-miniport-adapter"></a>停止微型端口适配器





从系统中删除适配器并停止硬件时，NDIS 会调用 NDIS 微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数来释放资源。 当驱动程序的[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数成功返回后，NDIS 可以调用*MiniportHaltEx* 。 有关 *MiniportInitializeEx*的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。

[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 必须释放驱动程序为设备分配的任何资源。 驱动程序必须调用**Ndis<em>Xxx</em> **函数的 reciprocals，它最初为资源分配了资源。 作为一般规则， *MiniportHaltEx*函数应按初始化期间使用的相反顺序调用倒数**Ndis<em>Xxx</em> **函数。

如果适配器生成中断，则会在*MiniportHaltEx*禁用中断之前，使用该驱动程序的[*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)函数来抢占微型端口驱动程序的[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。

如果存在未完成的 OID 请求或发送请求，NDIS 不会调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 。 Ndis 调用 *MiniportHaltEx*后，ndis 不会对受影响的设备发出进一步的请求。

[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)返回后，微型端口驱动程序将处于暂停状态。

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序停止处理程序](halt-handler.md)

[编写 NDIS 微型端口驱动程序](./initializing-a-miniport-driver.md)

 

