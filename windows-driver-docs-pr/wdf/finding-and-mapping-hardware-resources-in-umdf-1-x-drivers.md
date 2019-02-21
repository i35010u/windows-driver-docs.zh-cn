---
title: 查找和映射硬件资源在 UMDF 1.x 驱动程序
description: 查找和映射硬件资源在 UMDF 1.x 驱动程序
ms.assetid: 51CB254D-1B2C-43F5-925A-209810E2F5FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c5268c4512da8a60573f2229e5076f2c1a9457
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555532"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>查找和映射硬件资源在 UMDF 1.x 驱动程序


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果使用 UMDF 2.0 或更高版本，请参阅[查找和映射硬件资源](finding-and-mapping-hardware-resources.md)。

UMDF 1.x 驱动程序接收中的硬件资源及其[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)回调方法。 驱动程序使用[ **IWDFCmResourceList** ](https://msdn.microsoft.com/library/windows/hardware/hh439762)界面，用于查看翻译的资源列表和识别内存映射寄存器、 I/O 端口和中断。

该驱动程序通过调用循环资源列表[ **IWDFCmResourceList::GetCount** ](https://msdn.microsoft.com/library/windows/hardware/hh439767)并[ **IWDFCmResourceList::GetDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/hh439771).

如果该驱动程序收到内存映射寄存器，驱动程序必须调用[ **IWDFDevice3::MapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/hh451225)映射寄存器之后它才能访问它们。 通常情况下，驱动程序映射中的其寄存器及其[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)方法。 该驱动程序取消映射中的注册其[ **IPnpCallbackHardware2::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439739)通过调用回调[ **IWDFDevice3::UnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/hh451237). 请注意，对于 I/O 端口不需要映射。

有关演示如何将驱动程序查找和内存映射的映射注册资源的示例，请参阅[ **IWDFDevice3::MapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/hh451225)。

 

 





