---
Description: The Windows Hardware Lab Kit (HLK) tests can be used for additional testing of Systems, USB host controllers, hubs, and devices.
title: 有关 USB 的 Windows 硬件实验室 Kit (HLK) 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4ece82c5267b85db8cd658dddbe6191fb43a479
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524389"
---
# <a name="windows-hardware-lab-kit-hlk-tests-for-usb"></a>有关 USB 的 Windows 硬件实验室 Kit (HLK) 测试


Windows 硬件 Lab Kit (HLK) 测试可以用于其他测试系统、 USB 主控制器、 中心和设备。 这些测试涵盖基本的设备功能、 可靠性和与 Windows 兼容性。

## <a name="prerequisites"></a>必备条件


在之前运行的徽标测试开始请确保满足以下要求：

-   若要运行这些测试将需要至少两台计算机： 测试服务器和测试客户端。
-   测试客户端必须具有 Windows 的最新版本。
-   测试客户端必须具有 EHCI 和 xHCI 控制器，集成或作为外接卡。 控制器必须公开用户可访问根端口 （无集成中心）。
-   下载到测试服务器从 Windows HLK [Windows 硬件实验室工具包下载](https://go.microsoft.com/fwlink/p/?linkid=285647)。

    有关如何安装和使用 Windows HLK 的详细信息，请参阅[Windows HLK Getting Started](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

## <a name="hardware-requirements-for-running-usb-tests-in-the-hlk"></a>在 HLK 中运行 USB 测试的硬件要求


若要运行 HLK 测试，需要：

-   主控制器 （集成或作为外接卡）、 中心或设备进行认证。

    测试客户端上打开设备管理器，并确保你想要使用的 USB 控制器公开用户可访问根端口 （无集成中心）。

    ![usb 根端口](images/roothubports.png)

-   USB 如果符合外部 SuperSpeed 集线器，以便评估系统的兼容性。 我们测试了使用这些中心的 HLK 测试：
    -   [Texas Instruments SuperSpeed (USB 3.0) 中心参考设计板 (TUSB8040EVM)](https://go.microsoft.com/fwlink/p/?linkid=248509)。
    -   SuperMUTT 包。 请参阅[MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。
-   [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)一样测试集线器和控制器测试设备。
-   USB-如果认证电缆和连接器，以便避免信号完整性问题。 请参阅[USB-如果产品列表](https://go.microsoft.com/fwlink/p/?linkid=617502)。

此处给出完整的要求集：

-   [USB 总线控制器测试先决条件](https://go.microsoft.com/fwlink/p/?linkid=617477)
-   [USB Hub.Connectivity 测试先决条件](https://go.microsoft.com/fwlink/p/?linkid=617499)

## <a name="hlk-test-selection-for-usb"></a>有关 USB 的 HLK 测试选择


适用于你的系统、 主机控制器、 集线器或设备的 USB 测试会自动选择 HLK Studio 中。

请按照步骤 1 到 5 后[Windows HLK Getting Started]( https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)，请确保：

-   在步骤 5 中，在中选择正确的设备**选择**HLK Studio 选项卡。
-   在步骤 6 中，将应用于你的设备的所有测试中都显示**测试**HLK studio 中的选项卡。 若要运行这些测试，您必须在左侧的复选框中选择该测试，并单击**运行所选项**。 本文档的以下部分列出了 USB 测试的测试。

有关计划的测试的信息，请参阅中的步骤 2-6 [Windows HLK Getting Started]( https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

## <a name="recommended-windows-hlk-tests"></a>推荐的 Windows HLK 测试

除了所有 USB 测试 HLK Studio 中自动选择的我们都建议运行测试以及使用 MUTT 或 SuperMUTT 连接到系统、 控制器或测试下的中心的基础知识。 用于系统提交它们的系统基础知识 (SysFund) 测试，这些都是设备基础 （说明） 测试控制器、 中心或设备提交。

-   [系统基础知识 (SysFund)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/system-fundamentals-tests)
-   [设备基础 （说明）](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-tests)

## <a name="related-topics"></a>相关主题
[在 Windows 中测试 USB 硬件、 驱动程序和应用程序](usb-driver-testing-guide.md)  



