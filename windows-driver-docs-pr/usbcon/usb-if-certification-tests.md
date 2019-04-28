---
Description: 若要准备的 Windows 硬件认证计划提交的 USB 设备和主机控制器的硬件供应商和设备制造商的指南。
title: USB-IF 认证测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b5169c89d717d031dc5e43f0b7e548ba717cf6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330371"
---
# <a name="usb-if-certification-tests"></a>USB-IF 认证测试


若要准备的 Windows 硬件认证计划提交的 USB 设备和主机控制器的硬件供应商和设备制造商的指南。

## <a name="usb-if-certification-tests"></a>USB-IF 认证测试


如果制造 USB 硬件，特别是 USB 设备或主机控制器，您的硬件必须满足 USB 的电气和机械要求-如果为了接收 Windows 认证。 USB-如果认证涵盖的 USB 设备和主机控制器的更多深入测试，并确保高质量实现。

早期版本的 Windows 硬件认证工具包所需硬件制造商将提交到 USB 设备-如果用于测试。 但是，该要求已更改。 不再需要提交到 USB 设备-如果用于测试。

HLK，USB 的新版本-如果测试要求允许供应商下载并从 USB 运行的测试-如果网站，然后添加这些测试已通过在 HLK 中。 如果已认证设备通过 USB-如果你需要提供 USB 的设备对 HLK 的 IF 测试 ID (TID)。

即使 USB 设备通过当前 Microsoft Windows 认证计划要求，其中许多设备不完全符合 USB 规范。 最常见示例包括：

-   **中心**:通常会失败，因为它们报告它们具有外部电源时它们实际上只具有总线能力。 False 报表会导致无效的电压条件在总线上。
-   **硬盘驱动器**:通常失败，因为它们不正确地枚举由于从 USB 总线过量的功率绘图。 在许多情况下，这些硬盘磁盘驱动器都需要非标准电缆才能正常工作。
-   **闪存驱动器**:通常会失败，因为它们正确; 不处理描述符请求这将导致设备挂起或失败的 Microsoft 操作系统描述符。
-   **卡读取器**:通常失败，因为它们不进入的选择性挂起状态。
-   **打印机**:通常失败，因为它们不从待机状态恢复。
-   **音频**:通常失败，因为它们不从待机状态恢复。

糟糕的用户体验、 困难公共关系、 产品返回和丢失的收入、 高产品的支持呼叫量、 和与维护服务已发货的产品中的错误关联的成本增加，可能会导致不符合标准的 USB 设备。
## <a name="windows-hlk-requirements-for-usb-if-tests"></a>USB Windows HLK 要求-IF 测试


-   设备 (**Device.Connectivity.UsbDevices.UsbifCertification)**

    我们强烈建议 USB-如果证书;但是，Windows HLK 要求**Device.Connectivity.UsbDevices.UsbifCertification**不再需要 USB-如果认证的 USB 设备。 要求状态，设备可以是任一 USB-如果认证，或子集 USB-如果的认证测试可以在设备上运行。

-   托管控制器 (**Device.BusController.UsbController.UsbifCertification**)

    USB 主机控制器制造商必须获取完整的 USB-如果以符合其各自的 Windows HLK 要求的证书。

-   中心 (**Device.Connectivity.UsbDevices.UsbifCertification**)

    USB 集线器制造商必须获取完整的 USB-如果以符合其各自的 Windows HLK 要求的证书。

当用户选择 USB 主控制器，若要将集成到他们的系统时，应注意这些要求的系统制造商。 与 USB 设备，这些要求可以显著提高客户体验。 它们可以帮助防止崩溃和挂起，主要原因，并减少进行故障排除和调试非合规性问题所花费的时间。

## <a name="windows-hardware-certification-submission-options"></a>Windows 硬件认证提交选项


此图显示了如何获取 Windows 认证的处理流程。

![usb-如果测试](images/usbif-testing.png)

您可以提交 Windows 认证资格，以满足新 USB 的 USB 设备-如果通过使用以下方法之一来测试要求：

- **USB-如果认证**

  获取 USB-从如果认证[USB-如果授权独立的测试实验室](http://www.usb.org/developers/compliance/labs/)，并提交针对 Windows 证书认证设备。 您可以选择以下选项之一来获取 USB-如果认证的设备或主机控制器：

  -   提交到 USB 设备-如果授权用于测试的独立的测试实验室。 有关如何查找实验室的信息，请参阅 USB-如果授权独立的测试实验室。
      **请注意**通常所花费的已授权的独立测试实验室一到两周测试 USB 规范的单个 USB 设备。

         

  -   要提交供 USB 的 USB 设备向已授权的独立测试实验室-如果认证制造商必须注册到实验室并具有有效的供应商 ID (VID)。

  设备已成功通过 USB 后-如果认证测试，则必须在设备的以下权限：

  -   可以在你的设备的手册、 打包和产品信息的使用 USB 徽标。
  -   你可以列出 USB 上-如果集成商列表。
  -   将设备引入[USB 如果赞助法规遵从性研讨会](http://www.usb.org/developers/events/compshop/)。 每年在美国，保留四个学习班，并且一个研讨会保存在亚洲。

  设备通过 USB 后的认证测试，如果您收到来自测试实验室或研讨会的测试 ID 数量 (TID)。 在运行 Windows HLK 测试设备的其余部分时，可以向 Windows HLK 提供此 TID 数字。

  测试和认证 USB 设备在授权独立的测试实验室的成本而异实验室实验室。 某些授权单独的测试实验室会提供批量折扣或一些关联的企业的折扣。 没有任何费用，若要测试和认证的 USB 设备在任何 USB 如果赞助法规遵从性研讨会。 您必须是 USB 的成员-如果参加 USB-如果赞助法规遵从性研讨会。

- **USB-如果自我测试**

  下载 USB 命令验证工具测试工具和 USB 互操作性测试文档，并运行从所需的测试[USB-如果](http://www.usb.org/home)。 然后提交针对 Windows 证书认证设备。

  **请注意**USB 主控制器和中心均不适合 USB-如果自测试选项，必须获取完整的 USB-如果认证。

  如果您决定使用 USB-如果自检选项来获取 Windows 认证，你必须至少执行下列 USB-IF 测试：

  -   USB 命令验证工具进行测试：USB 命令验证工具测试来验证设备以了解并接受 USB 的常用命令的能力。
  -   USB 互操作性测试：USB 互操作性测试的目标的功能和设备能够与其他 USB 外围设备共存。

  下载和外部 Windows HLK 运行这些测试。 请注意，必须仅最新版本的 Windows 上运行这些测试 (所指定的 USB-如果)，即使您在提交您针对 Windows 的多个版本的 Windows 证书认证的 USB 设备。 测试结果适用于所有版本的 Windows 的所有 Windows 认证提交。

  以下步骤介绍如何执行所需的 USB-IF 测试才能符合 Windows 认证的设备。

  1. 下载 USB 3.0 命令验证工具测试工具 (USB30CV) 和互操作性测试中的文档[SuperSpeed USB 软件和硬件工具](https://go.microsoft.com/fwlink/p/?LinkId=623333)。
  2. 运行 USB-IF 测试下表中指定的 USB 硬件：

     <table>
     <colgroup>
     <col width="50%" />
     <col width="50%" />
     </colgroup>
     <thead>
     <tr class="header">
     <th>USB 版本</th>
     <th>USB-IF 测试</th>
     </tr>
     </thead>
     <tbody>
     <tr class="odd">
     <td>USB 2.0</td>
     <td><p>附加后 xHCI 主控制器的设备并运行 USB 3.0 命令验证工具测试工具 (USB30CV) 中的一章 9 测试 [USB 2.0 设备]。</p>
     <p>EHCI 一部分的互操作性部分中所述运行互操作性测试<a href="http://compliance.usb.org/resources/GoldSuite%20Test%20Procedure.pdf">GoldSuite 测试过程文档</a>。 两次运行这些测试： 一个与 EHCI 主控制器，后面附加设备，然后随附背后 xHCI 主控制器的设备。</p></td>
     </tr>
     <tr class="even">
     <td>USB 3.0</td>
     <td><p>附加后 xHCI 主控制器的设备并运行 USB 3.0 命令验证工具测试工具 (USB30CV) 中的一章 9 测试 [USB 3.0 设备]。</p>
     <p>运行互操作性测试，如中所述<a href="https://go.microsoft.com/fwlink/p/?LinkId=623335" data-raw-source="[XHCI Interoperability Testing](https://go.microsoft.com/fwlink/p/?LinkId=623335)">XHCI 互操作性测试</a>文档。 运行这些测试两次： 一次，后面 EHCI 主控制器，连接的设备和随附背后 xHCI 主控制器的设备的一次。</p></td>
     </tr>
     </tbody>
     </table>
    
  3. 如果已通过测试输入字符串"SELFTEST"作为测试 ID (TID) 输入到 USB-IF HLK 中的证书验证测试。

## <a name="related-topics"></a>相关主题
[有关 USB 的 Windows 硬件实验室工具包测试](windows-hardware-certification-kit-tests-for-usb.md)  



