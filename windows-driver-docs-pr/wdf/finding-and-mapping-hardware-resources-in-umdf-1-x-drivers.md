---
title: 在 UMDF 1.x 驱动程序中查找和映射硬件资源
description: 在 UMDF 1.x 驱动程序中查找和映射硬件资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63a59c5bc8a6b557267e77de7b4cc1c8ff43429f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815743"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中查找和映射硬件资源


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果使用的是 UMDF 版本2.0 或更高版本，请参阅 [查找和映射硬件资源](finding-and-mapping-hardware-resources.md)。

UMDF 1.x 驱动程序通过其 [**IPnpCallbackHardware2：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware) 回调方法接收硬件资源。 驱动程序使用 [**IWDFCmResourceList**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist) 接口查看翻译后的资源列表，并识别内存映射的寄存器、i/o 端口和中断。

驱动程序通过调用 [**IWDFCmResourceList：： GetCount**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfcmresourcelist-getcount) 和 [**IWDFCmResourceList：： GetDescriptor**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfcmresourcelist-getdescriptor)来循环访问资源列表。

如果驱动程序接收内存映射寄存器，则驱动程序必须调用 [**IWDFDevice3：： MapIoSpace**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace) 来映射寄存器，然后才能访问它们。 通常，驱动程序会在其 [**IPnpCallbackHardware2：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware) 方法中映射其寄存器。 驱动程序通过调用 [**IWDFDevice3：： UnmapIoSpace**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-unmapiospace)在其 [**IPnpCallbackHardware2：： OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)回调中 messagebox 取消寄存器。 请注意，i/o 端口不需要映射。

有关演示驱动程序如何查找和映射内存映射寄存器资源的示例，请参阅 [**IWDFDevice3：： MapIoSpace**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)。

 

