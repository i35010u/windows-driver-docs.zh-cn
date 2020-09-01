---
title: 协议驱动程序中的可分页和可丢弃代码
description: 协议驱动程序中的可分页和可丢弃代码
ms.assetid: acc27690-cdc3-433c-85c4-489501ea3d26
keywords:
- 协议驱动程序 WDK 网络，可分页和可放弃代码
- NDIS 协议驱动程序 WDK、可分页和可放弃代码
- 可分页和可放弃代码 WDK NDIS 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691b20399f607341efa6433f9e88a9a78e2961fb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211005"
---
# <a name="pageable-and-discardable-code-in-a-protocol-driver"></a>协议驱动程序中的可分页和可丢弃代码





驱动程序开发人员应尽可能将代码指定为可分页，为必须驻留在内存中的代码释放系统空间。 可以用 [**NDIS 可 \_ 分页 \_ 函数**](/previous-versions/windows/hardware/network/ff557121(v=vs.85)) 宏将函数标记为可分页。 函数的 IRQL、资源管理功能和其他特性可能禁止该函数被分页。

每个 *ProtocolXxx* 函数在被动 \_ 级别和调度级别范围内的 IRQL 范围内运行 \_ 。 仅以 IRQL = 被动级别运行的函数 \_ 应标记为可分页。

只要运行的驱动程序函数既不调用 \_ 也不由以 irql = 调度级别运行的任何函数 &gt; \_ （例如获取旋转锁的函数）调用，则可以将其作为可分页的驱动程序函数进行分页。 获取旋转锁将导致获取线程的 IRQL 引发到调度 \_ 级别。 如果驱动[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)程序函数被标记为可分页代码，则在 IRQL = 被动级别运行的驱动程序函数 \_ 不能调用任何以 irql = 调度级别运行的**Ndis * Xxx*** 函数 &gt; \_ 。 有关每个 **ndis * Xxx*** 函数的 IRQL 的详细信息，请参阅 [Ndis 库函数](/previous-versions/windows/hardware/network/ff557039(v=vs.85))。

NDIS 协议驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数以及仅从 **DriverEntry**调用的代码应使用 [**NDIS \_ INIT \_ function**](/previous-versions/windows/hardware/network/ff557007(v=vs.85)) 宏指定为仅初始化代码。 使用此宏标识的代码假定在系统初始化时只运行一次，因此，仅在该时间映射。 标记为初始化的函数返回后，将被丢弃。

 

