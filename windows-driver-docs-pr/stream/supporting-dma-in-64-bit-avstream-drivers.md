---
title: 在 64 位 AVStream 驱动程序中支持 DMA
description: 在 64 位 AVStream 驱动程序中支持 DMA
keywords:
- AVStream WDK，硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
- 64位 WDK AVStream
- 32位可寻址设备 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c9cb7fce66e08bbb35bfdd1ac3f3e669ae104cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839833"
---
# <a name="supporting-dma-in-64-bit-avstream-drivers"></a>在 64 位 AVStream 驱动程序中支持 DMA





AVStream 支持32位和64位可寻址设备上的 DMA。

为 Win64 平台编译的所有驱动程序应使用 [**IKsDeviceFunctions：： RegisterAdapterObjectEx**](/windows-hardware/drivers/ddi/ks/nf-ks-iksdevicefunctions-registeradapterobjectex) 而不是 [**KsDeviceRegisterAdapterObject**](/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)。

**IKsDeviceFunctions：： RegisterAdapterObjectEx** 仅在 Microsoft Windows SERVER 2003 SP1 及更高版本中可用。

下面的代码示例演示了如何在基于 x64 的客户端版本和32位平台上支持 DMA：

```cpp
NTSTATUS MyDeviceStart (...) {
// Get the DMA adapter object and store it in the Context member of the I/O stack location.
Context -> AdapterObject = IoGetDmaAdapter (
Device -> PhysicalDeviceObject,
&DeviceDesc,
&Context -> NumberOfMapRegisters
);

PUNKNOWN DeviceUnk =
KsDeviceGetOuterUnknown (
Device
);

// Register the DMA adapter with AVStream
IKsDeviceFunctions *DeviceFunctions;
NTSTATUS Status = DeviceUnk -> QueryInterface (
__uuidof (IKsDeviceFunctions),
(PVOID *)&DeviceFunctions
);

// Conditionally, call IksDeviceFunctions::RegisterAdapterObjectEx, 
// which will not break downlevel load compatibility.

if (NT_SUCCESS (Status)) {
DeviceFunctions -> RegisterAdapterObjectEx (
Context -> AdapterObject,
&DeviceDesc,
Context -> NumMapRegisters,
MAX_MAPPING,
sizeof (KSMAPPING)
);
DeviceFunctions -> Release ();
}

// If this call fails, call KsDeviceRegisterAdapterObject to
// preserve downlevel load compatibility.
else {
KsDeviceRegisterAdapterObject (
Device,
Context -> AdapterObject,
MAX_MAPPING,
sizeof (KSMAPPING)
);
}
...
```

此代码示例适用于64位和32位平台。 如果驱动程序找不到 **IKsDeviceFunctions：： RegisterAdapterObjectEx**，它仍然会调用 **KsDeviceRegisterAdapter**。

此外，在创作64位 AVStream 驱动程序时，最大限度地减少持有的并发帧锁的数量。 由于 AVStream 在微型驱动程序第一次锁定帧时生成了散点/集合映射，因此，如果不遵循此准则，驱动程序可能会耗尽资源。 特别是，如果您要编写一个要在包含32位卡的 Win64 平台上运行的驱动程序，增加锁的数目会使锁定失败的几率增加，因为内存缓冲区不足是有限的资源。

 

