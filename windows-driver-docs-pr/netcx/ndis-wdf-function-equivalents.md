---
title: NDIS WDF 函数等效项
description: NDIS WDF 函数等效项
ms.assetid: 28C8DFA3-5602-422D-89AA-6EA05F501E15
keywords:
- NetAdapterCx NDIS WDF 函数等效项，NetCx NDIS WDF 函数等效项
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2647f9c0a06a7637189c4e431b726d9ba75b7633
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545741"
---
# <a name="ndis-wdf-function-equivalents"></a>NDIS WDF 函数等效项

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

下表列出了 NDIS 函数和其 WDF 等效项：

|NDIS API 系列|WDF 等效项|
|-|-|
|[**NdisAllocateIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff561604)|[**WdfWorkItemCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551201)|
|[**NdisAllocateTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561618)|[**WdfTimerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550050)|
|[**NdisAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff560699)|[**WdfSpinLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff550040)|
|[**NdisInterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff562752)|[**InterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff547910)|
|[**NdisInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562732)|[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)|
|[**NdisMInitializeScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff553543)|[**WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)|
|[**NdisInitializeString**](https://msdn.microsoft.com/library/windows/hardware/ff562741)|[**WdfStringCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550046)|
|[**NdisSystemActiveProcessorCount**](https://msdn.microsoft.com/library/windows/hardware/ff564577)|[**KeGetCurrentProcessorNumberEx**](https://msdn.microsoft.com/library/windows/hardware/ff552076) (kernel)|
|[**NdisWriteRegisterUchar**](https://msdn.microsoft.com/library/windows/hardware/ff564678)|[**WDF_WRITE_REGISTER_UCHAR**](https://msdn.microsoft.com/library/windows/hardware/dn265684)|
