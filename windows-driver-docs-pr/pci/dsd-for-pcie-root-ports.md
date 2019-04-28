---
title: PCIe 根端口的设备特定数据 (_DSD)
description: ACPI _DSD 方法可支持现代待机和 PCI 热插入方案
ms:assetid: 44ad67da-f374-4a8e-80bd-d531853088a2
keywords: ACPI、 ACPI \_DSD 方法
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9746d3bc2f43bbc6e82e580261b3380386cb956
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352941"
---
# <a name="acpi-interface-device-specific-data-dsd-for-pcie-root-ports"></a>ACPI 接口：PCIe 根端口的设备特定数据 (_DSD)

在 Windows 10 (版本 1803) 中，已添加新的 ACPI _DSD 方法以支持现代待机和 PCI 热插拔方案：
## <a name="directed-deepest-runtime-idle-platform-state-drips-support-on-pcie-root-ports"></a>定向 PCIe 根端口上支持的最深运行时空闲平台状态 (DRIPS) 

 必须启用新式备用的桌面系统上用户可以访问每个 PCIe 根端口/槽的 ACPI 作用域中实现此 ACPI 对象。 

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

此 ACPI 对象允许操作系统来识别和电源管理 PCIe 根端口能够处理在 D3 状态的热插拔事件。 如果此对象未实现上 PCIe 热插入支持端口，则系统不会电源管理此端口，如果它没有任何子级 PCIe 设备，从而导致系统使用比实际所需的更多能力。

此对象必须实现上运行时 D3 Thunderbolt™ 层次结构的所有 PCIe 根端口上 (RTD3) 支持系统根端口 ACPI 设备作用域中的。

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

此 ACPI 对象允许操作系统以标识外部公开的 PCIe 层次结构 (例如 Thunderbolt™)。 此对象必须实现根端口 ACPI 设备作用域中。

注意：在系统上使用 Windows 10 1803年传送，这只应实现 PCIe Thunderbolt™ 层次结构的根端口上。

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
## <a name="see-also"></a>请参阅

[启用 PCI 高速本机控制在 Windows 中](enabling-pci-express-native-control.md)
