---
title: 访问 PCI 设备配置空间
description: 访问 PCI 设备配置空间
keywords:
- PCI 配置空间 WDK 总线
- 配置空间 WDK 总线
- IRP_MN_READ_CONFIG
- IRP_MN_WRITE_CONFIG
ms.date: 08/31/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9ef90d3fb6230acdc0e1f716f1df10900ceb65ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812561"
---
# <a name="accessing-pci-device-configuration-space"></a>访问 PCI 设备配置空间


 (PCI) 设备上的外围组件互连上的某些操作是为设备的功能驱动程序预留的。 例如，此类操作包括访问总线的设备特定配置空间，并 (DMA) 控制器对直接内存访问进行编程。 Microsoft 通过两种方法为访问 PCI 设备的配置空间提供系统支持：

-   [**总线 \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)总线接口

-   配置 i/o 请求数据包 (Irp) 、 [**IRP \_ MN \_ 读取 \_ 配置**](../kernel/irp-mn-read-config.md) 和 [**IRP \_ MN \_ 写入 \_ 配置**](../kernel/irp-mn-write-config.md)

>[!NOTE]
>从 Windows 10、2004开始，如果设备具有 (SDEV 的安全设备) 启用了 ACPI 表并启用了基于虚拟化的安全性，则会对访问 PCI 设备配置空间的不受支持的方法施加限制。 如果驱动程序或进程尝试使用上面未列出的方法读取或操作 PCI 设备配置空间，则该访问将被阻止，并将导致系统 bug 检查。

Windows XP 和 Windows Server 2003 及更高版本的操作系统可以独占控制 *PCI 本地总线* 规范定义的配置空间标头以及功能链接列表中的所有功能。 驱动程序不得尝试修改这些寄存器。

但是，驱动程序可以使用 IRP \_ MN \_ 写入 \_ 配置请求或总线接口标准的 **SetBusData** 方法， \_ 将不属于该标头的配置空间写入到供应商定义的功能列表 \_ 。 驱动程序还可以使用 IRP \_ MN \_ read \_ CONFIG 请求或总线接口标准的 **GetBusData** 方法读取 \_ 设备的功能 \_ 。 若要使用 IRP \_ MN \_ READ \_ config 或 IRP \_ MN \_ WRITE \_ CONFIG，驱动程序必须在被动 \_ 级别运行。 有关驱动程序可以查询的功能列表和相应结构，请参阅 [PCI 结构](/windows-hardware/drivers/ddi/index) 部分。

驱动程序可以从扩展 PCI 设备配置空间读取 (也就是说，使用 IRP \_ MN \_ read \_ CONFIG 请求或总线接口标准的 **GetBusData** 方法时 \_ ，超过256字节的配置数据) \_ 。 同样，驱动程序可以使用 IRP \_ MN \_ 写入 \_ 配置请求或总线接口标准的 **SetBusData** 方法， \_ 写入扩展 PCI 设备配置空间 \_ 。 如果设备没有扩展配置空间或平台未定义设备上扩展配置空间的路径，则读取请求将返回0xFFFF 并且写入请求将不起作用。 若要确定操作是否成功，驱动程序可以检查读取或写入的字节数。

PCI Express 和 PCI-X 模式2支持大于256个字节的扩展 PCI 设备配置空间。 驱动程序可以读取和写入此配置空间，但仅支持相应的硬件和 BIOS 支持。 在 ACPI BIOS 中，根总线必须具有 PNP0A08 或 PNP0A03 的 PNP ID。 对于 PNP ID 为 PNP0A03 的根总线， \_ 具有函数4的 DSM 方法应指示当前模式为 pci-x 模式2。 所有桥和设备都应为 PCI express，或在 PCI-X 模式2中运行。

此外，系统应支持内存映射配置空间访问。 这是通过在系统 BIOS/固件中定义 MCFG 表。 Windows Vista 和 Windows Server 2008 及更高版本的操作系统会自动支持内存映射配置空间访问。

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

 

