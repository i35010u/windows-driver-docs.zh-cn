---
title: 在 64 位 AVStream 驱动程序中支持 DMA
description: 在 64 位 AVStream 驱动程序中支持 DMA
ms.assetid: 1173a83f-8d9e-4678-bfb5-f2fb91e827be
keywords:
- AVStream WDK 硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
- 64 位 WDK AVStream
- 32 位可寻址的设备 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2e2b07c6051ca8e4cd30e56786edde5030dc500
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382088"
---
# <a name="supporting-dma-in-64-bit-avstream-drivers"></a>在 64 位 AVStream 驱动程序中支持 DMA





AVStream 支持在 32 位和 64 位可寻址的设备上的 DMA。

Win64 平台应使用已编译的所有驱动程序[ **IKsDeviceFunctions::RegisterAdapterObjectEx** ](https://msdn.microsoft.com/library/windows/hardware/ff559852)而不是[ **KsDeviceRegisterAdapterObject**](https://msdn.microsoft.com/library/windows/hardware/ff561687).

**IKsDeviceFunctions::RegisterAdapterObjectEx**才可在 Microsoft Windows Server 2003 SP1 及更高版本。

下面的代码示例说明了如何在基于 x64 的客户端版本和 32 位平台上支持 DMA:

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

此代码示例适用于 64 位以及 32 位平台。 如果找不到驱动程序**IKsDeviceFunctions::RegisterAdapterObjectEx**，它仍调用**KsDeviceRegisterAdapter**。

此外，在创作时 64 位 AVStream 驱动程序，最大程度减少并发框架持有的锁的数量。 由于 AVStream 生成散播-聚集映射微型驱动程序第一次锁定帧时，您的驱动程序可能用完资源，如果未遵循此原则。 具体而言，如果正在编写了 32 位卡 Win64 平台上运行的驱动程序，增加的同时进行的锁的数量会增加锁将失败，因为较低的内存缓冲区是一种有限的资源的可能性。

 

 




