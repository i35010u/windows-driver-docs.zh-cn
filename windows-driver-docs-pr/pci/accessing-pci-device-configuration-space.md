---
title: 访问 PCI 设备配置空间
description: 访问 PCI 设备配置空间
ms.assetid: 05e0ada9-d465-4787-abc5-469a75352ee0
keywords:
- PCI 配置空间 WDK 总线
- 配置空间 WDK 总线
- IRP_MN_READ_CONFIG
- IRP_MN_WRITE_CONFIG
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65d7ced2c053cea016b909171b0250e8fe7dd4fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366126"
---
# <a name="accessing-pci-device-configuration-space"></a>访问 PCI 设备配置空间


外围组件互连 (PCI) 设备上的某些操作被保留的设备的功能驱动程序。 此类操作包括，例如，访问总线的特定于设备的配置空间和编程的直接内存访问 (DMA) 控制器。 Microsoft 提供系统支持通过两种方法访问 PCI 设备的配置空间：

-   [**总线\_界面\_标准**](https://msdn.microsoft.com/library/windows/hardware/ff540707)总线接口

-   配置 I/O 请求数据包 (Irp) [ **IRP\_MN\_读取\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)并[ **IRP\_MN\_编写\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551769)

Windows XP 和 Windows Server 2003 和更高版本操作系统有配置空间标头的独有控制由定义*PCI 本地总线*规范，以及所有的功能中的功能链接的列表。 驱动程序必须尝试修改这些寄存器。

但是，驱动程序可以写入不属于的标头或供应商定义的这使用 IRP 的功能列表的配置空间\_MN\_编写\_配置请求或**SetBusData**总线方法\_接口\_标准。 驱动程序还可以阅读使用设备的功能，使用 IRP\_MN\_读取\_配置请求或者**GetBusData**总线方法\_接口\_标准。 若要使用 IRP\_MN\_读取\_配置或 IRP\_MN\_编写\_的配置来说，驱动程序必须运行在被动\_级别。 有关功能和相应的驱动程序可以查询的结构的列表，请参阅[PCI 结构](https://msdn.microsoft.com/library/windows/hardware/ff537590)部分。

驱动程序可以读取扩展 PCI 设备配置空间 （即，超过 256 个字节的配置数据） 使用 IRP\_MN\_读取\_配置请求或者**GetBusData**方法总线\_接口\_标准。 同样，驱动程序可以写入其扩展 PCI 设备配置空间进行使用 IRP\_MN\_编写\_配置请求或**SetBusData**总线方法\_接口\_标准。 如果设备不具有扩展的配置空间或平台的设备上未定义的扩展的配置空间的路径，读取的请求将返回 0xFFFF 和写入请求不会产生影响。 若要确定如果操作成功，驱动程序可以检查读取或写入的字节的数。

PCI Express 和 PCI X 模式 2 支持大于 256 个字节的扩展的 PCI 设备配置空间。 驱动程序可以读取和写入到此配置的空间，而只使用适当的硬件和 BIOS 支持。 在 ACPI BIOS 中，根总线必须具有 PNP0A08 或 PNP0A03 的即插即用 ID。 对于使用即插即用 ID 的 PNP0A03，根总线\_函数 4 DSM 方法应指示当前模式是 PCI X 模式 2。 所有的桥和设备应为 PCI express 或在 PCI X 模式 2 操作。

此外，系统应支持内存映射配置空间访问。 这是通过在系统 BIOS/固件中定义 MCFG 表。 Windows Vista 和 Windows Server 2008 和更高版本操作系统自动支持内存映射配置空间访问。

下面的代码示例演示如何查询设备的电源管理功能数据：

```cpp
#define LSZ sizeof(ULONG)
#define HEADERSIZE (FIELD_OFFSET (PCI_COMMON_CONFIG, DeviceSpecific)) / LSZ

 // The PCI_COMMON_CONFIG structure includes 
// device specific data. The following
// structure is used to retrieve the
// 64 bytes of data that precedes the
// device-specific data.

typedef struct {
    ULONG  Reserved[HEADERSIZE];
} PCI_COMMON_HEADER, *PPCI_COMMON_HEADER;

PCI_COMMON_HEADER Header;
PCI_COMMON_CONFIG *pPciConfig = (PCI_COMMON_CONFIG *)&Header;
// declare power management capabilities header
 PCI_PM_CAPABILITY  PowerMgmtCapability;
PCI_PM_CAPABILITY  *pPowerMgmtCapability = &Capability; 
UCHAR CapabilityOffset;

// Read the first part of the header
// to get the status register and
// the capabilities pointer.
// The "capabilities pointer" is
// actually an offset from the
// beginning of the header to a
// linked list of capabilities.
BusInterface.GetBusData(Context,
    PCI_WHICHSPACE_CONFIG,
    pPciConfig, // output buffer
    0, // offset of the capability to read
 sizeof(PCI_COMMON_HEADER)); // just 64 bytes

// Check the Status register to see if 
// this device supports capability lists.
 
if ((pPciConfig->Status &
   PCI_STATUS_CAPABILITIES_LIST) == 0) {
   // does not support capabilities list
   return(STATUS_NOT_IMPLEMENTED);
}

// The device supports capability lists.
// Find the capabilities.

// The position of the capabilities pointer
// in the header depends on whether this is 
// a bridge type device. Check the type.

if ((pPciConfig->HeaderType & 
   (~PCI_MULTIFUNCTION)) == PCI_BRIDGE_TYPE) {
   CapabilityOffset = 
       pPciConfig->u.type1.CapabilitiesPtr;
} else if ((pPciConfig->HeaderType & 
   (~PCI_MULTIFUNCTION)) == PCI_CARDBUS_TYPE) {
   CapabilityOffset = 
       pPciConfig->u.type2.CapabilitiesPtr;
} else {
   CapabilityOffset = 
       pPciConfig->u.type0.CapabilitiesPtr;
}

// Loop through the capabilities in search
// of the power management capability. The
// list is NULL-terminated, so the last 
// offset will always be zero.

while (CapabilityOffset != 0) {

    // Read the header of the capability at 
    // this offset.

    // If the retrieved capability is not
    // the power management capability that
    // we are looking for, follow the
    // link to the next capability and
    // continue looping.

    BusInterface.GetBusData(Context,
        PCI_WHICHSPACE_CONFIG,
        pPowerMgmtCapability,
        CapabilityOffset,
        sizeof(PCI_CAPABILITIES_HEADER));

    if (Capability->Header.CapabilityID ==
 PCI_CAPABILITY_ID_POWER_MANAGEMENT) {
        // Found the power management capability
        break;
    } else {
        // This is some other capability.
        // Keep looking for the power 
        // management capability.
        CapabilityOffset = Capability->Header.Next;
    }
}

if (CapabilityOffset == 0) {
    // We didn't find a power management
    // capability. Return an error.
    return(STATUS_NOT_IMPLEMENTED);
}

// Skip past the capabilities header and read
// the rest of the power management capability

BusInterface.GetBusData(Context,
   PCI_WHICHSPACE_CONFIG,
   // write to location immediately following header
   & (pPowerMgmtCapability->Header) + 1, 
   CapabilityOffset + 
       sizeof(PCI_CAPABILITIES_HEADER),
   sizeof(PCI_PM_CAPABILITY) - 
       sizeof(PCI_CAPABILITIES_HEADER)
);
```

 

 




