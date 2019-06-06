---
title: 将总线相对地址映射到虚拟地址
description: 将总线相对地址映射到虚拟地址
ms.assetid: 16496465-8a30-4250-9d64-afd36a788ae2
keywords:
- 虚拟地址空间映射 WDK 内核
- 物理地址空间映射 WDK 内核
- 映射内存
- 地址空间映射 WDK 内核
- 转换地址空间 WDK 内核
- 内存管理 WDK 内核，地址映射
- 总线相对内存空间 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0059597bf2b3c96bf58ffeb24605ca8d36959da0
ms.sourcegitcommit: e542212bb5e7aba06b9e005e9b63c438404d5643
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719954"
---
# <a name="mapping-bus-relative-addresses-to-virtual-addresses"></a>将总线相对地址映射到虚拟地址





某些处理器实现单独的内存和 I/O 地址空间，而其他处理器不能。 由于这些差异的硬件平台，用于访问 I/O-或-驻留在内存中设备的资源不同平台的机制驱动程序。

驱动程序将请求响应即插即用设备 I/O 和内存资源管理器的[ **IRP\_MN\_查询\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff551715) IRP。 根据硬件体系结构，HAL 可以分配在 I/O 空间或内存空间中的 I/O 资源，并且可以分配内存资源在 I/O 空间或内存空间中。

如果 HAL 使用总线相对内存空间以访问设备资源 （例如设备注册），驱动程序必须到虚拟内存映射 I/O 空间，以便它可以访问这些资源。 该驱动程序可以确定资源是否通过检查由即插即用管理器在设备启动时传递给驱动程序的已翻译的资源是 I/O 或内存驻留。 如果 HAL 使用 I/O 空间，则需要无映射。

具体而言，当驱动程序收到[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求，它应检查在结构**IrpSp&gt;Parameters.StartDevice.AllocatedResources**并**IrpSp-&gt;Parameters.StartDevice.AllocatedResourcesTranslated**，描述原始 （总线相对） 和已翻译的资源分别分配给设备的即插即用的管理器。 驱动程序应该将每个资源列表的副本保存设备扩展中，为帮助调试。

资源列表成对[ **CM\_资源\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff541994)结构，其中原始列表的每个元素对应于已翻译的列表的相同元素。 例如，如果**AllocatedResources.List**\[0\]描述原始的 I/O 端口范围**AllocatedResourcesTranslated.List**\[0\]介绍翻译后的相同的范围。 每个已翻译的资源包括物理地址和资源的类型。

如果驱动程序分配的已翻译的内存资源 (**CmResourceTypeMemory**)，必须调用[ **MmMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff554618)物理地址映射到通过虚拟地址它可以访问设备注册。 对于以独立于平台的方式运行的驱动程序，它应检查已翻译的每个返回的资源并绘制其地图，如有必要。

**内核模式驱动程序应采取以下步骤中，以响应 IRP\_MN\_启动\_设备请求，以确保所有设备资源的访问权限**

1.  复制**IrpSp-&gt;Parameters.StartDevice.AllocatedResources**到设备扩展。

2.  复制**IrpSp-&gt;Parameters.StartDevice.AllocatedResourcesTranslated**到设备扩展。

3.  在循环中，检查的每个描述符元素**AllocatedResourcesTranslated**。 如果描述符资源类型为**CmResourceTypeMemory**，调用**MmMapIoSpace**，传递的物理地址和长度的已翻译的资源。

当驱动程序收到[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)或[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738) PnP 管理器中，从请求它必须通过调用释放映射[ **MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)类似循环中。 该驱动程序还应调用**MmUnmapIoSpace**如果必须故障**IRP\_MN\_启动\_设备**请求。

原始资源类型指示驱动程序应调用哪个 HAL 访问例程 (**READ_REGISTER_* XXX * * *，**WRITE_REGISTER_* XXX * * *，**READ_PORT_* XXX * * *，**WRITE_PORT_* XXX * * *)。 大多数驱动程序不需要检查原始资源列表，以确定哪个例程使用，因为驱动程序本身请求的资源或驱动程序编写器知道所需考虑设备硬件的特性的类型。

 在 I/O 空间中的资源 (**CmResourceTypePort**， **CmResourceTypeInterrupt**， **CmResourceTypeDma**)，该驱动程序应使用所返回的低阶 32 位物理地址来访问设备的资源，例如，通过 HAL 的读取和写入 **READ_REGISTER_* XXX * * *，**WRITE_REGISTER_* XXX * * *，**READ_PORT_* XXX * * *， **WRITE_PORT_ * XXX*** 例程。
 
 

 




