---
title: NDIS-WDF 函数等效项
description: NDIS-WDF 函数等效项
ms.assetid: 28C8DFA3-5602-422D-89AA-6EA05F501E15
keywords:
- NetAdapterCx NDIS-WDF 函数等效项，NetCx NDIS-WDF 函数等效项
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0401c17459ce3b745d33cf64084c88deae86dbb4
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210807"
---
# <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 函数等效项

下表列出了 NDIS 函数及其 WDF 等效项：

|NDIS API 系列|WDF 等效项|
|-|-|
|[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)|[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)|
|[**NdisAllocateTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatetimerobject)|[**WdfTimerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)|
|[**NdisAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)|[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))|
|[**NdisInterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedincrement)|[**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)|
|[**NdisInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent)|[**KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)|
|[**NdisMInitializeScatterGatherDma**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553543(v=vs.85))|[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)|
|[**NdisInitializeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializestring)|[**WdfStringCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringcreate)|
|[**NdisSystemActiveProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissystemactiveprocessorcount)|[**KeGetCurrentProcessorNumberEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumberex) （内核）|
|[**NdisWriteRegisterUchar**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteregisteruchar)|[**WDF_WRITE_REGISTER_UCHAR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/nf-wdfhwaccess-wdf_write_register_uchar)|
