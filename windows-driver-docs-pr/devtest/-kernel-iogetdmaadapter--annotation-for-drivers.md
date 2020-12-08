---
title: 驱动程序的 _Kernel_IoGetDmaAdapter_ 注释
description: 使用 _Kernel_IoGetDmaAdapter_ 注释指示代码分析工具查找是否误用 DMA 指针。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0af3f02347df3f7d563ec691e95b83d8d9a41820
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795157"
---
# <a name="_kernel_iogetdmaadapter_-annotation-for-drivers"></a>\_\_ \_ 驱动程序的内核 IoGetDmaAdapter 批注


使用 \_ 内核 \_ IoGetDmaAdapter \_ 批注指示代码分析工具查找是否误用 DMA 指针。

如果函数调用使用 \_ 内核 IoGetDmaAdapter 批注批注的接口 \_ \_ ，则它应具有重试逻辑，以便重试发生，直至函数成功。

IoGetDmaAdapter 例程返回的寄存器数可能少于请求数，要求调用方继续使用实际数量，而不是请求的数目。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)

 

 






