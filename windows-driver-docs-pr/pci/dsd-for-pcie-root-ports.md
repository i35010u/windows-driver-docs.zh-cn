---
title: PCIe 根端口的设备特定数据 (_DSD)
description: 用于支持新式备用和 PCI 热插拔方案的 ACPI _DSD 方法
ms:assetid: 44ad67da-f374-4a8e-80bd-d531853088a2
keywords: ACPI，ACPI \_ DSD 方法
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: d7f9f7c218fe3596b261240a3af8a32a8ffeb4cc
ms.sourcegitcommit: 985439ba501a870675a8bd6867c4b8944cc002d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84225968"
---
# <a name="acpi-interface-device-specific-data-_dsd-for-pcie-root-ports"></a>ACPI 接口： \_ 适用于 PCIe 根端口的设备特定数据（DSD）

在 Windows 10 （版本1803）中，新增了 ACPI \_ DSD 方法来支持新式备用和 PCI 热插拔方案。

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

此 ACPI 对象使操作系统能够识别和管理能够在 D3 状态下处理热插拔事件的 PCIe 根端口。 如果未在 PCIe 热插拔可用端口上实现此对象，则系统不会对此端口进行电源管理，因为它没有任何子 PCIe 设备，导致系统消耗的电量比所需的更多。

此对象必须在根端口 ACPI 设备范围内的闪电层次结构的所有 PCIe 根端口（在运行时 D3 （RTD3）的系统）上实现。

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

此 ACPI 对象使操作系统能够识别外部公开的 PCIe 层次结构，如闪电。 此对象必须在根端口 ACPI 设备范围内实现。

注意：在 Windows 10 版本1803的系统发货上，此对象只应在闪电层次结构的 PCIe 根端口上实现。

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

## <a name="identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection"></a>确定用户可访问并需要 DMA 保护的内部 PCIe 端口

此 ACPI 对象使操作系统能够识别可供用户轻松访问的内部 PCIe 层次结构（例如，使用闩锁可以访问的便携式计算机 M. 2 PCIe 槽），并需要由 OS[内核 DMA 保护](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)机制进行保护。 此对象必须在根端口 ACPI 设备范围内实现。

注意的重要事项：

- 仅 Windows 10 版本1903及更高版本支持使用此 ACPI 对象保护 PCI 端口。

- 必须在系统 BIOS/UEFI 中启用内核 DMA 保护，操作系统才能分析 \_ DSD 并将必要的保护应用到 PCI 端口。

- 连接到此端口的设备的驱动程序必须支持 DMA 重新映射，否则，Windows 10 可能会阻止这些设备运行，直到用户登录或无限期，具体取决于[DMAGuard 策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard)。

```asl
Name (_DSD, Package () {  

ToUUID("70D24161-6DD5-4C9E-8070-705531292865"),
Package () {
Package (2) {"DmaProperty", 1}, // Property 1: This port needs to be protected by the OS
Package (2) {"UID", 0}, // Property 2: UID of the PCIe port on platform, range is: 0, 1, …, n-1
                   }
        }
)
```

## <a name="identifying-pcie-ports-supporting-d3_cold_aux_power-ecn-interface"></a>识别支持 D3_COLD_AUX_POWER ECN 接口的 PCIe 端口

此 ACPI 对象使操作系统能够识别支持[D3_COLD_AUX_POWER ECN 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_d3cold_aux_power_and_timing_interface)的 pcie 端口，这允许 pcie 设备从平台上的其他辅助电源，在默认375mA 上进行请求 @3.3V 。 定义此 DSD 的任何 PCI 端口或桥*都必须*保证在对以前协商的辅助电源值进行编程时，操作将会成功。

```asl
Name (_DSD, Package () {
            ToUUID("6B4AD420-8FD3-4364-ACF8-EB94876FD9EB"),
            Package () {
            }
        }
)

```

## <a name="see-also"></a>请参阅

[在 Windows 中启用 PCI Express 原生控制](enabling-pci-express-native-control.md)

[闪电3的内核 DMA 保护](https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt)

[D3COLD_AUX_POWER_AND_TIMING_INTERFACE 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_d3cold_aux_power_and_timing_interface)
