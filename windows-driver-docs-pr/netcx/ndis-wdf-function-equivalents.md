---
title: NDIS-WDF 函数等效项
description: NDIS-WDF 函数等效项
keywords:
- NetAdapterCx NDIS-WDF 函数等效项，NetCx NDIS-WDF 函数等效项
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0be1f39014e231bc586b4609b9b91b4efb3032c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838851"
---
# <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 函数等效项

下表列出了 NDIS 函数及其 WDF 等效项：

|NDIS API 系列|WDF 等效项|
|-|-|
|[**NdisAllocateIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)|[**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)|
|[**NdisAllocateTimerObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)|[**WdfTimerCreate**](/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)|
|[**NdisAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)|[**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))|
|[**NdisInterlockedIncrement**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedincrement)|[**InterlockedIncrement**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)|
|[**NdisInitializeEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent)|[**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)|
|[**NdisMInitializeScatterGatherDma**](/previous-versions/windows/hardware/network/ff553543(v=vs.85))|[**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)|
|[**NdisInitializeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializestring)|[**WdfStringCreate**](/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringcreate)|
|[**NdisSystemActiveProcessorCount**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissystemactiveprocessorcount)|[**KeGetCurrentProcessorNumberEx**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumberex) (内核) |
|[**NdisWriteRegisterUchar**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteregisteruchar)|[**WDF_WRITE_REGISTER_UCHAR**](/windows-hardware/drivers/ddi/wdfhwaccess/nf-wdfhwaccess-wdf_write_register_uchar)|
