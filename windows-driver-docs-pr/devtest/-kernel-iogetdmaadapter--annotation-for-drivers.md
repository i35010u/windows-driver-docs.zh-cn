---
title: _Kernel_IoGetDmaAdapter_驱动程序的批注
description: 使用_Kernel_IoGetDmaAdapter_要直接查找不恰当使用 DMA 指针的代码分析工具中的批注。
ms.assetid: 51F71815-D899-48F5-8F81-92B139FC6B8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa3e56cdfd451749b45dfb6dd360249c5f03db7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547347"
---
# <a name="kerneliogetdmaadapter-annotation-for-drivers"></a>\_内核\_IoGetDmaAdapter\_驱动程序的批注


使用\_内核\_IoGetDmaAdapter\_要直接查找不恰当使用 DMA 指针的代码分析工具中的批注。

如果一个函数调用接口使用批注\_内核\_IoGetDmaAdapter\_批注，它应具有如此一来，就会重试该函数成功之前，进行重试逻辑。

IoGetDmaAdapter 例程无法返回请求的寄存器中，数少于和调用方才能继续使用的实际数目，不请求的数。

```ManagedCPlusPlus
_Must_inspect_result_
_IRQL_requires_max_(PASSIVE_LEVEL)
NTKERNELAPI
struct _DMA_ADAPTER *
IoGetDmaAdapter(
    _In_opt_ PDEVICE_OBJECT PhysicalDeviceObject,           // required for PnP drivers
    _In_ struct _DEVICE_DESCRIPTION *DeviceDescription,
    _Out_ _When_(return!=0, _Kernel_IoGetDmaAdapter_ _At_(*NumberOfMapRegisters, _Must_inspect_result_))
    PULONG NumberOfMapRegisters
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[SAL 2.0 注释 Windows 驱动程序](sal-2-annotations-for-windows-drivers.md)

 

 






