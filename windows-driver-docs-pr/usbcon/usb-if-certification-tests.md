---
Description: 适用于硬件供应商和设备制造商的指南，用于为 Windows 硬件认证计划提交准备 USB 设备和主机控制器。
title: USB-IF 认证测试
ms.date: 10/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9577c09b317b4a632101764e1de35c0124c51b7c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210601"
---
# <a name="usb-if-certification"></a>USB-IF 证书

适用于硬件供应商和设备制造商的指南，用于为 Windows 硬件认证计划提交准备 USB 设备和主机控制器。

## <a name="usb-if-certification-tests"></a>USB-IF 认证测试

USB 硬件（特别是 USB 设备或主机控制器）必须满足 USB 的电气和机械要求-如果要接收 Windows 认证。 USB-如果证书包含更深入的 USB 设备和主机控制器测试，并确保实现高质量的实现。

更早版本的 Windows 硬件认证工具包需要制造商将其设备提交到 USB-如果测试。 新版本的 HLK、USB-如果测试要求允许制造商从 USB-IF 网站下载并运行测试，然后在 HLK 中断言这些测试已传入。 如果你的设备已被 USB-IF 认证，则需要为设备向设备提供 USB IF 测试 ID （TID）。

即使 USB 设备通过了当前的 Microsoft Windows 认证计划要求，其中许多设备也不能完全遵守 USB 规范。 最常见的示例包括：

- **集线器**：通常会失败，因为它们报告它们在实际只有总线电源时具有外部电源。 错误报告将导致总线上出现无效电压情况。
- **硬盘驱动器**：常见的原因是由于 USB 总线的功率消耗过多而无法正确枚举。 在许多情况下，这些硬盘驱动器需要非标准电缆才能正常工作。
- **闪存驱动器**：通常会因不正确地处理描述符请求而失败;这会导致设备挂起，并使 Microsoft 操作系统描述符失败。
- **卡读取器**：通常会因为未进入 "选择性挂起" 状态而失败。
- **打印机**：通常会因为无法从待机状态恢复而失败。
- **音频**：常见失败，因为它们不会从待机状态恢复。

不符合的 USB 设备可能会导致用户体验不佳、难于公共关系、产品退货、高产品支持呼叫量，以及与交付产品中的服务错误关联的成本增加。

## <a name="windows-hlk-requirements-for-usb-if-tests"></a>适用于 USB 的 Windows HLK 要求-IF 测试

- 设备（**UsbDevices. UsbifCertification）**：

    强烈建议采用 USB-IF 认证;但是，Windows HLK 要求**UsbDevices。 UsbifCertification**不再需要 usb 设备的 usb 证书。 要求表明设备可以是 USB 设备，也可以是 usb （如果已经过认证），也可以在设备上运行 USB 假设的认证测试的子集。

- 主机控制器（**BusController. UsbController. UsbifCertification**）

    为了满足各自的 Windows HLK 要求，USB 主机控制器制造商必须获取完整的 USB 证书。

- 集线器（**UsbDevices. UsbifCertification**）

    为了满足各自的 Windows HLK 要求，USB 集线器制造商必须获取完整的 USB-IF 证书。

当系统制造商选择要集成到系统中的 USB 主机控制器时，应了解这些要求。 这些要求可显著改善客户体验 USB 设备。 它们有助于防止崩溃和挂起的关键原因，并缩短排查和调试不符合性问题所花费的时间。

## <a name="windows-hardware-certification-submission-options"></a>Windows 硬件认证提交选项

此图显示了如何获取 Windows 证书的过程流程。

![usb-if 测试](images/usbif-testing.png)

你可以使用以下方法之一提交用于 Windows 认证限定的 USB 设备，以满足新的 USB-IF 测试要求：

- **USB-IF 证书**

  从 Usb 获取 USB-如果[授权独立测试实验室](https://www.usb.org/labs)，然后提交设备以进行 Windows 认证资格。 你可以选择以下选项之一来获取设备或主机控制器的 USB-IF 证书：

  - 将设备提交到 USB 设备，以用于测试。 有关如何查找实验室的信息，请参阅 USB-如果授权独立测试实验室。
      **注意** 它通常需要一个到两周的授权独立测试实验室来测试单个 USB 设备是否符合 USB 规范。

  - 若要将 USB 设备提交给授权的、适用于 USB 的独立测试实验室（如果是认证），制造商必须向实验室注册，并且具有有效的供应商 ID （VID）。

  设备成功通过 USB-如果认证测试后，你将拥有以下设备权限：

  - 你可以使用 USB 徽标获取设备的手册、打包和产品信息。
  - 可以在 "USB-IF 集成商" 列表中列出。
  - 将设备带到[USB 赞助合规性研讨会](https://www.usb.org/upcoming-events)。 每年，美国的四个讨论会都已举行，其中一场讨论会保存在亚洲。

  设备通过 USB-IF 认证测试后，将从测试实验室或讨论会接收测试 ID 号（TID）。 当你为设备运行其余的 Windows HLK 测试时，向 Windows HLK 提供此 TID 编号。

  在授权的独立测试实验室中测试和验证 USB 设备的成本可能因实验室而异。 某些授权的独立测试实验室为一些关联企业提供批量折扣或折扣。 在任何带任何 USB 的符合性研讨会上测试和认证 USB 设备不收取任何费用。 你必须是 USB-IF 的成员才能参加 USB-IF 赞助合规性研讨会。

- **USB-如果自测试**

  下载 USB 命令验证程序测试工具和 USB 互操作性测试文档，并从[USB-IF](https://usb.org/usb32tools)运行所需的测试。 然后提交设备以进行 Windows 认证。

 >**注意**： usb 主机控制器和集线器不符合 USB-if 自测试选项的条件，必须获取完整的 usb 证书。

  如果你决定使用 USB-IF 自测试选项来获取 Windows 认证，则至少必须执行以下 USB 测试：

  - USB 命令验证器测试： USB 命令验证器测试可验证设备理解和接受常见 USB 命令的能力。
  - USB 互操作性测试： USB 互操作性测试面向设备与其他 USB 外围设备共存的功能和能力。

  这些测试是在 Windows HLK 之外下载和运行的。 请注意，这些测试必须仅在最新版本的 Windows 上运行（如 USB-IF 所指定），即使你要为 windows 的多个版本提交适用于 Windows 认证的认证。 测试结果适用于所有版本的 Windows 的所有 Windows 认证提交。

  以下步骤介绍如何执行所需的 USB-IF 测试来限定设备进行 Windows 认证。

  1. 从[Usb 软件和硬件工具](https://usb.org/usb32tools)下载 Usb 命令验证器测试工具（USB3CV）和互操作性测试文档。

  2. 按下表中指定的方式运行 usb 硬件测试：

  | USB 版本 | USB-IF 测试 |
  | --- | --- |
  | USB 2.0 | 在 xHCI 主机控制器后面附加设备，并在 USB 3.0 命令验证器测试工具（USB3CV）中运行第9章测试 [USB 2.0 设备]。 <br><br> 按照[Ehci 测试过程](https://compliance.usb.org/resources/GoldSuite%20Test%20Procedure.pdf)的 "互操作性" 部分的 "ehci 部分" 中所述运行互操作性测试。 运行这些测试两次：一次用于连接到 EHCI 主机控制器后面的设备，然后连接到 xHCI 主机控制器后面的设备。 |
  | USB 3.0 | 在 xHCI 主机控制器后面附加设备，并在 USB 3.0 命令验证器测试工具（USB3CV）中运行第9章测试 [USB 3.0 设备]。 <br><br> 运行[XHCI 互操作性测试过程](https://www.usb.org/document-library/xhci-interoperability-test-procedures-peripherals-hubs-and-hosts-version-096)文档中所述的互操作性测试。 两次运行以下测试：一次将设备连接到 EHCI 主机控制器之后，一次将设备连接到 xHCI 主机控制器。 |
  
  3. 如果测试通过，则在 HLK 中输入字符串 "SELFTEST" 作为 "USB-IF" 认证验证测试的 "测试 ID （TID）" 输入。

## <a name="related-topics"></a>相关主题

[适用于 USB 的 Windows 硬件实验室包测试](windows-hardware-certification-kit-tests-for-usb.md)
