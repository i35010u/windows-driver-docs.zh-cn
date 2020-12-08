---
title: PCI 电源管理和设备驱动程序
description: 阐明了遵循 PCI 电源管理 (的硬件如何) 与设备驱动程序交互。
ms.date: 12/04/2001
ms.localizationpriority: medium
ms.openlocfilehash: d08f3f359ad937407f0e56eb5829a2d417ebea01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812537"
---
# <a name="pci-power-management-and-device-drivers"></a>PCI 电源管理和设备驱动程序

本文阐明了一些供应商已遇到的一些混乱情况，即供应商遇到的有关使用 pci 电源管理的硬件如何 (PCI-X) 与操作系统中的设备驱动程序进行交互，以及如何将 PCI-X 与 ACPI 集成。 有关详细信息，请参阅 [https://www.uefi.org/specifications](https://www.uefi.org/specifications)

## <a name="device-drivers-and-pci-power-management"></a>设备驱动程序和 PCI 电源管理

本讨论假设你熟悉 Windows 驱动模型 (WDM) 驱动程序如何处理电源管理事件，如当前的 Windows DDK 中所述。 通常，设备驱动程序的责任如下：

- **总线驱动程序**：总线驱动程序负责枚举、配置和控制设备。 对于 PCI-X，PCI 驱动程序负责读取 PCI-X 寄存器，确定硬件的功能。 当电源 Irp 请求电源状态发生更改时，PCI 驱动程序将写入 PCI 电源管理寄存器，以将硬件设置为不同 Dx 状态。

   如果为设备启用了唤醒，PCI 驱动程序将写入 PCI-X 注册，使设备能够激发 PME (ACPI 还将执行一项操作，请参阅下一节) 。 最后，当 ACPI 确定 PCI 总线正在唤醒系统时，PCI 驱动程序会扫描 PCI 配置空间，查找哪个设备正在断言 PME，在该设备上禁用 PME，并通知该设备的驱动程序。

- **设备驱动程序**：设备的特定驱动程序负责保存和还原设备上下文，并请求电源状态更改，作为设备的策略所有者。 如果设备驱动程序收到请求较低设备电源状态更改的电源 IRP，则设备驱动程序将负责保存稍后启用设备所需的任何专有设备上下文。 在某些情况下，可能没有要保存的内容。

PCI-X 注册严格是 PCI 驱动程序的域--IHV 的设备驱动程序不需要访问这些寄存器中的任何一个。 这样做会导致系统无法可靠地工作。 设备驱动程序的责任是只执行专用操作。

## <a name="integrating-acpi-and-pci-pm"></a>集成 ACPI 和 PCI PM

某些设备，尤其是笔记本中的主板视频设备，可能需要 PCI 电源管理以及 ACPI 源语言组装器 (ASL) 才能完全管理设备。 PCI 电源管理寄存器将控制设备的内部状态，如内部时钟和电源平面。 ASL 将控制外部状态，例如外部时钟和电源平面; 对于视频控制器，ASL 将控制视频 backlights。 请注意，ASL 和 PCI-X 只能组合在主板设备上。

OnNow 体系结构是分层体系结构，处理设备驱动程序、PCI 驱动程序和 ACPI 驱动程序的集成， (和 ASL) 自然。 下面的方案演示了调用驱动程序来处理这些设备的顺序。

>[!NOTE]
>为了使上述方案按照说明进行操作，WDM 驱动程序必须按照当前版本的 Microsoft Windows DDK 中所述正确转发 POWER Irp。

## <a name="scenario-1-turning-off-a-device"></a>方案1：关闭设备

1. **设备驱动程序**：保存专有设备状态。
2. **PCI 驱动程序**：保存即插即用配置，禁用设备 (中断和条) ，并使用 pci-x 注册将设备置于 D3。
3. **ACPI 驱动程序**：运行 ASL 代码 (\_ PS3 和 \_ OFF，以便不再使用电源资源) 控制芯片的外部状态。

## <a name="scenario-2-pci-power-management-and-device-drivers"></a>方案2： PCI 电源管理和设备驱动程序

1. **ACPI 驱动程序**：运行 ASL 代码 (\_ PS0，对 \_ 任何 OnNow 所需的功率资源) 控制芯片的外部状态。
2. **Pci 驱动程序**：使用 pci-x 注册将设备置于 D0，并还原即插即用配置 (中断和条--它们可能与设备以前) 的内容不同。
3. **设备驱动程序**：还原设备中的专有上下文。

## <a name="scenario-3-enabling-wake-up"></a>方案3：启用唤醒

1. **设备驱动程序**：设置芯片中的专有寄存器以启用唤醒。 例如，在模式匹配网络唤醒中，这是将模式编程到适配器的时候。
2. **Pci 驱动程序**：在 PCI PM 注册中设置唤醒，使设备能够断言 PME。
3. **ACPI 驱动程序**：启用与 PME 关联的芯片集中的 GPE (如 \_ 根 PCI 总线) 中列出的 PRW 对象所述。

## <a name="scenario-4-wake-up"></a>方案4：唤醒

1. **ACPI 驱动程序**：唤醒和扫描 GPE 状态位以实现唤醒事件，禁用 GPEs 以设置 GPE 状态位，以及运行 \_ \_ 与 set Exx bits 关联的任何 Lxx 或 GPE 方法。 为了响应 PCI 总线上的唤醒通知，ACPI 驱动程序将完成 PCI 驱动程序的等待 \_ 唤醒 IRP，通知 pci 驱动程序它正在唤醒系统。
2. **PCI 驱动程序**：扫描配置空间，查找任何具有设置的 PME 状态位的设备。 对于每个设备，它会禁用 PME 并完成等待 \_ 唤醒 IRP，使该设备通知驱动程序正在断言唤醒状态。 PCI 驱动程序停止扫描唤醒设备，因为它已完成通过所有 PCI 设备，但找不到任何断言 PME 和 PME 停止断言。
3. **设备驱动程序**：请求将设备置于 D0 (参阅方案 2) ，并设置处理唤醒事件所需的芯片中的任何专有寄存器。

## <a name="call-to-action-on-pci-power-management-and-device-drivers"></a>对 PCI 电源管理和设备驱动程序的操作调用

- 按照本文中的说明将 ACPI 和 PCI-E PM 功能集成到你的设备中。
- 中提供了 PCI 电源管理规范 <https://www.pcisig.com> 。 此链接将离开 Microsoft.com 站点。
- ACPI 规范可在中找到 <https://www.uefi.org/specifications> 。 此链接将离开 Microsoft.com 站点。
- 可以在中找到 ACPI 组件体系结构 (ACPICA) 编译器 [https://acpica.org/downloads/binary-tools](https://acpica.org/downloads/binary-tools) 。
