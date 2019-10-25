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
ms.openlocfilehash: ae5aa75a6611d953ce40f1708fae594ffb4dcf96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843703"
---
# <a name="pageable-and-discardable-code-in-a-protocol-driver"></a>协议驱动程序中的可分页和可丢弃代码





驱动程序开发人员应尽可能将代码指定为可分页，为必须驻留在内存中的代码释放系统空间。 可以通过[**NDIS\_可分页\_函数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557121(v=vs.85))宏将函数标记为可分页。 函数的 IRQL、资源管理功能和其他特性可能禁止该函数被分页。

每个*ProtocolXxx*函数都在从被动\_级别到调度\_级别的范围内以 IRQL 为间隔运行。 仅以 IRQL = 被动\_级别运行的函数应标记为可分页。

只要运行的驱动程序\_函数既不调用也不由以 IRQL &gt;= 调度\_级别（例如获取旋转锁的函数）调用的任何函数调用，则可以将其设为可分页。 获取旋转锁将导致引发线程的 IRQL，以调度\_级别。 如果该驱动程序函数标记为可分页代码，则在 IRQL = 被动\_级别下运行的驱动程序函数（如[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)）不得调用以 irql &gt;= 调度\_级别运行的任何**Ndis * Xxx*** 函数。 有关每个**ndis * Xxx*** 函数的 IRQL 的详细信息，请参阅[Ndis 库函数](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557039(v=vs.85))。

使用[**ndis\_INIT\_function**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557007(v=vs.85))宏，ndis 协议驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数以及仅从**DriverEntry**调用的代码应指定为仅初始化代码。 使用此宏标识的代码假定在系统初始化时只运行一次，因此，仅在该时间映射。 标记为初始化的函数返回后，将被丢弃。

 

 





