---
title: 在 UMDF 1.x 驱动程序中查找和映射硬件资源
description: 在 UMDF 1.x 驱动程序中查找和映射硬件资源
ms.assetid: 51CB254D-1B2C-43F5-925A-209810E2F5FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eea8153e4841644dad27bb2cb165312318670a7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368713"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>在 UMDF 1.x 驱动程序中查找和映射硬件资源


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果使用 UMDF 2.0 或更高版本，请参阅[查找和映射硬件资源](finding-and-mapping-hardware-resources.md)。

UMDF 1.x 驱动程序接收中的硬件资源及其[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)回调方法。 驱动程序使用[ **IWDFCmResourceList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfcmresourcelist)界面，用于查看翻译的资源列表和识别内存映射寄存器、 I/O 端口和中断。

该驱动程序通过调用循环资源列表[ **IWDFCmResourceList::GetCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfcmresourcelist-getcount)并[ **IWDFCmResourceList::GetDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfcmresourcelist-getdescriptor).

如果该驱动程序收到内存映射寄存器，驱动程序必须调用[ **IWDFDevice3::MapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)映射寄存器之后它才能访问它们。 通常情况下，驱动程序映射中的其寄存器及其[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)方法。 该驱动程序取消映射中的注册其[ **IPnpCallbackHardware2::OnReleaseHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onreleasehardware)通过调用回调[ **IWDFDevice3::UnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-unmapiospace). 请注意，对于 I/O 端口不需要映射。

有关演示如何将驱动程序查找和内存映射的映射注册资源的示例，请参阅[ **IWDFDevice3::MapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-mapiospace)。

 

 





