---
title: 在 UMDF 1.x 驱动程序中查找和映射硬件资源
description: 在 UMDF 1.x 驱动程序中查找和映射硬件资源
ms.assetid: 51CB254D-1B2C-43F5-925A-209810E2F5FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41b05f64dd99141d113cec06befefab18b1edd06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842863"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中查找和映射硬件资源


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果使用的是 UMDF 版本2.0 或更高版本，请参阅[查找和映射硬件资源](finding-and-mapping-hardware-resources.md)。

UMDF 1.x 驱动程序通过其[**IPnpCallbackHardware2：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)回调方法接收硬件资源。 驱动程序使用[**IWDFCmResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)接口查看翻译后的资源列表，并识别内存映射的寄存器、i/o 端口和中断。

驱动程序通过调用[**IWDFCmResourceList：： GetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfcmresourcelist-getcount)和[**IWDFCmResourceList：： GetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfcmresourcelist-getdescriptor)来循环访问资源列表。

如果驱动程序接收内存映射寄存器，则驱动程序必须调用[**IWDFDevice3：： MapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)来映射寄存器，然后才能访问它们。 通常，驱动程序会在其[**IPnpCallbackHardware2：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)方法中映射其寄存器。 驱动程序通过调用[**IWDFDevice3：： UnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-unmapiospace)在其[**IPnpCallbackHardware2：： OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)回调中 messagebox 取消寄存器。 请注意，i/o 端口不需要映射。

有关演示驱动程序如何查找和映射内存映射寄存器资源的示例，请参阅[**IWDFDevice3：： MapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)。

 

 





