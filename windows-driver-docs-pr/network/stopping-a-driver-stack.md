---
title: 停止驱动程序堆栈
description: 停止驱动程序堆栈
ms.assetid: 2ecc0ebb-89d8-4cd8-ac1c-f9f1da7d2ca8
keywords:
- 驱动程序堆栈 WDK 网络，停止
- 停止驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 237cc4add053803b305d221c9e10ececdd963822
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214328"
---
# <a name="stopping-a-driver-stack"></a>停止驱动程序堆栈





如果删除了某个设备，NDIS 将停止驱动程序堆栈。 驱动程序堆栈停止操作按如下方式继续：

1.  NDIS 暂停驱动程序堆栈。 有关暂停驱动程序堆栈的详细信息，请参阅 [暂停驱动程序堆栈](pausing-a-driver-stack.md)。

2.  NDIS 调用协议驱动程序的 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数。

    绑定进入关闭状态。 完成 OID 和发送请求并返回所有接收数据后，绑定将进入未绑定状态。

3.  NDIS 从堆栈顶部开始向下移动到微型端口驱动程序，分离所有筛选器模块。

    在 NDIS 调用筛选器驱动程序的 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数，并且筛选器驱动程序释放筛选器模块的所有资源后，筛选器模块将处于已分离状态。

4.  NDIS 暂停微型端口适配器。

    当 NDIS 调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数后，微型端口驱动程序会释放微型端口适配器的所有资源，微型端口适配器将处于暂停状态。

5.  如果所有筛选器驱动程序的模块都已分离，则系统可以卸载筛选器驱动程序。

6.  如果微型端口驱动程序管理的所有微型端口适配器都被停止，则系统可以卸载微型端口驱动程序。

 

