---
title: PCIe 根端口的设备特定数据 (_DSD)
description: 用于支持新式备用和 PCI 热插拔方案的 ACPI _DSD 方法
ms:assetid: 44ad67da-f374-4a8e-80bd-d531853088a2
keywords: ACPI，ACPI \_DSD 方法
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 068544e52664ad138bac65aecc508dedbb174b76
ms.sourcegitcommit: 508e275021b34197fedd82b3649c9b59b471300b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "82039790"
---
# <a name="acpi-interface-device-specific-data-_dsd-for-pcie-root-ports"></a>ACPI 接口： PCIe 根端口的设备特定数据（_DSD）

在 Windows 10 （版本1803）中，新增了 ACPI _DSD 方法来支持新式备用和 PCI 热插拔方案：

## <a name="directed-deepest-runtime-idle-platform-state-drips-support-on-pcie-root-ports"></a>PCIe 根端口上的定向最深运行时空闲平台状态（DRIPS）支持

 此 ACPI 对象必须在每个 PCIe 根端口/槽的 ACPI 范围内实现，用户可在支持[定向电源管理框架（DFx）](../kernel/introduction-to-the-directed-power-management-framework.md)的新式备用系统上访问该系统。

```ASL
Name (_DSD, Package () {

          ToUUID("FDF06FAD-F744-4451-BB64-ECD792215B10"),

            Package () {

                Package (2) {"FundamentalDeviceResetTriggeredOnD3ToD0", 1},
            }
        }
)
```

## <a name="identifying-pcie-root-ports-supporting-hot-plug-in-d3"></a>在 D3 中识别支持热插拔的 PCIe 根端口

此 ACPI 对象允许操作系统识别和管理能够在 D3 状态下处理热插拔事件的 PCIe 根端口。 如果未在 PCIe 热插拔可用端口上实现此对象，则系统不会对此端口进行电源管理，因为它没有任何子 PCIe 设备，导致系统消耗的电量比所需的更多。

此对象必须在根端口 ACPI 设备作用域中的闪电™层次结构（运行时 D3 （RTD3）支持的系统）上实现。

```ASL
Name (_DSD, Package () {  

        ToUUID("6211E2C0-58A3-4AF3-90E1-927A4E0C55A4"),  

        Package () {  

            Package (2) {"HotPlugSupportInD3", 1},  

                   }
        }
)
```

## <a name="identifying-externally-exposed-pcie-root-ports"></a>识别外部公开的 PCIe 根端口

此 ACPI 对象允许操作系统识别外部公开的 PCIe 层次结构（例如，闪电™）。 此对象必须在根端口 ACPI 设备范围内实现。

注意：在 Windows 10 1803 系统交付的系统上，只应在闪电™层次结构的 PCIe 根端口上实现此操作。

```ASL
Name (_DSD, Package () {  

ToUUID("EFCC06CC-73AC-4BC3-BFF0-76143807C389"),
Package () {
Package (2) {"ExternalFacingPort", 1}, // Property 1: This is an externally facing port/hierarchy
Package (2) {"UID", 0}, // Property 2: UID of the externally facing port on platform, range is: 0, 1, …, n-1
                   }
        }
)
```

## <a name="see-also"></a>另请参阅

[在 Windows 中启用 PCI Express 原生控制](enabling-pci-express-native-control.md)
