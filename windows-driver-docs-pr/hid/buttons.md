---
title: HID 按钮驱动程序
description: 使用适用于 GPIO 按钮的 Microsoft 提供的按钮驱动程序;否则，请实现将 HID 数据注入操作系统的驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91151c196d6d2c44d9eda6ededc8486b9f8cdf59
ms.sourcegitcommit: 586b1844547359baca95e3228fa63fcba0b18608
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97096626"
---
# <a name="hid-button-drivers"></a>HID 按钮驱动程序

使用适用于 GPIO 按钮的 Microsoft 提供的按钮驱动程序;否则，请实现将 HID 数据注入操作系统的驱动程序。

按钮 (电源、窗口、音量和旋转锁定) 通常用于在改装或清单等窗体因素上，用户不能使用物理键盘时所发生的任务。 按钮通过提供 [hid 按钮报告描述符](../gpiobtn/hid-button-report-descriptors.md)将自己声明为作为 HID 设备的操作系统。 这使系统能够以标准化的方式解释这些按钮的用途和事件。 按钮状态发生更改时，该事件将映射到 [HID 用法](hid-usages.md)。 HID 传输微型驱动程序将这些事件报告给高级驱动程序，然后在用户模式或内核模式下将详细信息发送到 HID 客户端。

对于物理常规用途 i/o (GPIO) 按钮，HID 传输微型驱动程序是由 Microsoft 提供的内置驱动程序，它基于在定义的 GPIO 硬件资源上收到的中断报告事件。

内置驱动程序无法为未连接到中断线路的按钮服务。 对于此类按钮，你需要编写一个驱动程序，该驱动程序将该按钮作为 HID 按钮公开，并报告对 HID 类驱动程序的状态更改， (Microsoft 提供的) 。 驱动程序可以是 HID 源驱动程序，也可以是 HID 传输驱动程序。

## <a name="guidance-for-supporting-hid-buttons"></a>支持 HID 按钮的指南

下面是一些常规指针，可帮助你确定在创建 HID 按钮时应遵循的实现。

:::image type="content" source="images/button.png" alt-text="用于实现按钮的决策图" border="false":::

### <a name="use-the-microsoft-provided-in-box-button-driver"></a>使用 Microsoft 提供的内置按钮驱动程序

:::image type="content" source="images/hid-acpi.png" alt-text="HID 按钮的 ACPI 说明" border="false":::

如果要实现 GPIO 按钮，请描述系统 ACPI 中的按钮，以便 Windows 可以加载内置驱动程序 Hidinterrupt.sys，作为向操作系统报告事件的按钮驱动程序。

- [ACPI 按钮设备](acpi-button-device.md)
- [按钮行为](../gpiobtn/button-behavior.md)
- [Windows 10 核心版 ACPI 的示例按钮](acpi-button-device.md#sample-acpi-button-device-for-windows-10-core-os-editions)

Microsoft 建议尽可能使用内置传输微型驱动程序。

### <a name="write-a-hid-source-driver-in-kernel-mode"></a>在内核模式下编写 HID 源驱动程序

:::image type="content" source="images/hid-vhf.png" alt-text="使用虚拟 HID 框架的按钮" border="false":::

如果要实现非 GPIO 按钮，如需要由其他软件组件注入的 HID 格式的数据流，则可以选择写入内核模式驱动程序。 从 Windows 10 开始，你可以通过调用与虚拟 HID 框架 (VHF) 通信的编程接口来编写一个 HID 源驱动程序，并获取和设置与 HID 类驱动程序的 HID 报表。

- [如何编写与虚拟 HID Framework 交互 (VHF 的 HID 源驱动程序) ](virtual-hid-framework--vhf-.md)
- [虚拟 HID 框架参考](/windows-hardware/drivers/virtual-hid-framework--vhf-)

或者，你可以编写一个内核模式 HID 传输微型驱动程序，它受 Windows 早期版本支持。 但是，我们不建议采用这种方法，因为编写不当的 KMDF HID 传输微型驱动程序会导致系统崩溃。

- [传输微型驱动程序](transport-minidrivers.md)
- [HID 微型驱动程序 IOCTLs](/windows-hardware/drivers/ddi/_hid/#hid-class-driver-ioctls)

### <a name="write-a-umdf-hid-minidriver"></a>写入 UMDF HID 微型驱动程序

:::image type="content" source="images/hid-umdf.png" alt-text="HID 传输微型驱动程序" border="false":::

如果要实现非 GPIO 按钮，则可在用户模式下编写 HID 传输微型驱动程序，而不是使用前面编写的模型。 除了内核模式驱动程序和此驱动程序中的错误之外，这些驱动程序也不会检查整个系统。

- [创建 UMDF HID 微型驱动程序](../wdf/creating-umdf-hid-minidrivers.md)
- [UMDF HID 微型驱动程序 IOCTLs](/previous-versions/hh463977(v=vs.85))"

## <a name="universal-windows-drivers-for-hid-buttons"></a>HID 按钮的通用 Windows 驱动程序

从 Windows 10 开始，HID 驱动程序编程接口是 OneCoreUAP 的 Windows 版本的一部分。 通过使用这一组通用的接口，可以使用 [虚拟 HID 框架](/windows-hardware/drivers/ddi/_hid) 或 [传输微型驱动程序](transport-minidrivers.md) 接口编写按钮驱动程序。 这些驱动程序将在适用于桌面版的 Windows 10 上运行， (家庭版、专业版、企业版和教育版) 以及 Windows 10 移动版以及其他 Windows 10 版本。

有关分步指南，请参阅 [使用通用 Windows 驱动程序入门](/windows-hardware/drivers)。

## <a name="related-topics"></a>相关主题

[人体学接口设备](/windows-hardware/drivers/hid/)
