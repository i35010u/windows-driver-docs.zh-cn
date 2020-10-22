---
description: Windows 硬件实验室工具包 (HLK) 测试可用于其他系统、USB 主机控制器、集线器和设备测试。
title: 针对 USB 的 Windows Hardware Lab Kit (HLK) 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e05bedd543047713987adcba9bb30a18f4c4bc
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355993"
---
# <a name="windows-hardware-lab-kit-hlk-tests-for-usb"></a>针对 USB 的 Windows Hardware Lab Kit (HLK) 测试

Windows 硬件实验室工具包 (HLK) 测试可用于其他系统、USB 主机控制器、集线器和设备测试。 这些测试涵盖了基本的设备功能、可靠性以及 Windows 的兼容性。

## <a name="prerequisites"></a>必备条件

开始运行徽标测试之前，请确保满足以下要求：

- 若要运行这些测试，你将需要至少两台计算机：测试服务器和测试客户端。
- 测试客户端必须具有最新版本的 Windows。
- 测试客户端必须具有 EHCI 和 xHCI 控制器，其中集成了或作为附加卡。 控制器必须公开用户可访问的根端口， (没有集成的集线器) 。
- 从 [Windows 硬件实验室包](/windows-hardware/test/hlk/)下载下载 windows HLK 到测试服务器。

    有关如何安装和使用 Windows HLK 的详细信息，请参阅 [WINDOWS hlk 入门](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

## <a name="hardware-requirements-for-running-usb-tests-in-the-hlk"></a>在 HLK 中运行 USB 测试的硬件要求

若要运行 HLK 测试，需要：

- 主机控制器 (集成的或作为附加卡) 、集线器或设备进行身份验证。

    在测试客户端上打开设备管理器，并确保要使用的 USB 控制器公开用户可访问的根端口， (没有集成的中心) 。

    ![usb 根端口](images/roothubports.png)

- 与 USB 兼容的外部 SuperSpeed 集线器，用于评估系统兼容性。 我们已使用以下中心测试了一测试：
  - [德克萨斯州器材 SuperSpeed (USB 3.0) 集线器参考设计板 (TUSB8040EVM) ](https://www.ti.com/lit/ug/sllu130a/sllu130a.pdf)。
  - SuperMUTT Pack。 请参阅 [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。
  - [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md) 作为中心和控制器测试的测试设备。

下面提供了一组完整的要求：

- [USB 总线控制器测试先决条件](/windows-hardware/test/hlk/testref/usb-bus-controller-testing-prerequisites#:~:text=%20USB%20Bus%20Controller%20Testing%20Prerequisites%20%201,is%20required%20for%20USB%20host%20controller...%20More%20)
- [USB Hub.Connectivity 测试先决条件](/windows-hardware/test/hlk/testref/usb-hubconnectivity-testing-prerequisites)

## <a name="hlk-test-selection-for-usb"></a>用于 USB 的 HLK 测试选择

适用于你的系统、主机控制器、集线器或设备的 USB 测试会在 HLK Studio 中自动选择。

按照 [WINDOWS HLK 入门](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)中的步骤1-5 操作后，请确保：

- 在步骤5中，在 HLK Studio 的 " **选择** " 选项卡中选择了正确的设备。
- 在步骤6中，所有适用于你的设备的测试都显示在 HLK studio 的 " **测试** " 选项卡中。 若要运行这些测试，必须在左侧的复选框中选择测试，然后单击 " **运行所选项**"。 本文档的以下部分列出了对 USB 测试的测试。

有关计划测试的信息，请参阅 [WINDOWS HLK 入门]( /windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)中的步骤2-6。

## <a name="recommended-windows-hlk-tests"></a>推荐的 Windows HLK 测试

除了在 HLK Studio 中自动选择的所有 USB 测试外，我们还建议同时运行基础测试，并将 MUTT 或 SuperMUTT 连接到受测系统、控制器或集线器。 对于系统提交，这些是系统基础 (SysFund) 测试，对于控制器、中心或设备提交，这些是设备基础 (DevFund) 测试。

- [系统基础 (SysFund) ](/windows-hardware/test/hlk/testref/system-fundamentals-tests)
- [设备基础 (DevFund) ](/windows-hardware/test/hlk/testref/device-devfund-tests)

## <a name="related-topics"></a>相关主题

[Microsoft USB 测试工具 (MUTT) 设备的概述](/windows-hardware/drivers/usbcon/microsoft-usb-test-tool--mutt--devices)
