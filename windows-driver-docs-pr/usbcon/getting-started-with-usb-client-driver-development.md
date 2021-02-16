---
description: 本部分介绍 USB 驱动程序开发。
title: USB 客户端驱动程序开发的首要步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea82b4dcd90e97daaa148aa669bfdb11f0c09c1
ms.sourcegitcommit: 10c868384c77622e0444677c45b708f52fc24661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100542889"
---
# <a name="first-steps-for-usb-client-driver-development"></a>USB 客户端驱动程序开发的首要步骤

本部分介绍 USB 驱动程序开发概念和工具。 本部分适用于想要为 Microsoft 不提供内置驱动程序的 USB 设备的驱动程序开发的 devlopers 新的。 这些驱动程序在本文档中称为 *USB 客户端驱动程序* 。 本节中的主题介绍高级 USB 概念，并提供有关执行 USB 客户端驱动程序的常见任务的分步说明。 有关这些概念的详细信息，请参阅 [Usb 文档](https://usb.org/documents)中的 usb 规范。

驱动程序开发人员必须具有 c + + 编程语言的编码经验，并了解 *函数指针*、 *回调函数* 和 *事件处理程序* 的概念。 如果基于 User-Mode Driver Framework 编写驱动程序，开发人员必须熟悉 c + + 和 COM。

## <a name="learning-path-for-usb-client-driver-developers"></a>USB 客户端驱动程序开发人员的学习路径

1. 阅读 [USB 规范 3.2](https://usb.org/document-library/usb-32-specification-released-september-22-2017-and-ecns)。
    - 了解体系结构 (设备、主机控制器和中心) 的行业规范和不同组件。 务必了解数据流模型，主机和设备之间如何相互通信，以及设备所需的请求格式。

2. 获取测试 USB 设备。
     - 具有 USB 设备及其硬件规范。 该规范描述了设备功能和支持的供应商命令。 使用规范来确定设备驱动程序的功能以及相关的设计决策。

     - 如果使用 USB 驱动程序开发，请使用 [OSR USB FX2 学习工具包](https://www.amazon.com/OSR-USB-FX2-Learning-Kit/dp/B07FNSYCLR) 。 此工具包最适合学习本文档集中包括的 USB 示例。
     - 使用 Microsoft USB 测试工具 (MUTT) 设备。 可以从 [JJG 技术](http://www.jjgtechnologies.com/Mutt20.htm)购买 MUTT 硬件。 设备未安装安装的固件。 若要安装固件，请下载 [MUTT](./microsoft-usb-test-tool--mutt--devices.md)软件包。 有关详细信息，请参阅包附带的文档。

3. 研究 [usb 设备布局](usb-device-layout.md) 和相关的 [usb 描述符](usb-descriptors.md)。
    - 通过阅读配置描述符、每个受支持的备用设置的接口描述符及其终结点描述符来描述你的设备功能。 通过使用 [USBView](../debugger/usbview.md)，开发人员可以浏览所有 usb 控制器和连接到它们的 usb 设备，还可以检查设备配置。

4. [选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)
    - 确定驱动程序是否应为自定义驱动程序，或是否基于目标设备的设计使用 Microsoft 提供的驱动程序之一。 选择最佳驱动模式并描述每个模型支持的功能。

5. 查看 Microsoft 提供的 USB 驱动程序堆栈和驱动程序开发概念。
    - [Windows 中的 USB 主机端驱动程序](usb-3-0-driver-stack-architecture.md)。
    - [适用于所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。
    - [所有 USB 开发人员的概念](usb-concepts-for-all-developers.md)。
    - [设备节点和设备堆栈](../gettingstarted/device-nodes-and-device-stacks.md)。
    - 使用由 Orwick 和家伙编写的 *Windows Driver Foundation 开发驱动程序*。 有关详细信息，请参阅 [借助 WDF 开发驱动程序](../wdf/developing-drivers-with-wdf.md)。
    - [USB 驱动程序示例](usb-driver-samples-in-wdk.md)。
    - 了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将有助于做出适当的设计决策，并简化开发过程。
    - 区分用户模式和内核模式驱动程序体系结构模型。
    - 了解驱动程序加载以及 Windows 如何在设备树和设备节点中组织即插即用 (PnP) 设备。 开发人员还应了解 PnP 管理器如何生成设备堆栈以及驱动程序及其设备对象放置在设备堆栈中的位置。

6. 准备开发和调试环境。
    -  (WDK) 安装最新的 [Windows 驱动程序工具包 ](../download-the-wdk.md)。
    - [安装 Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/)。
    - [设置以进行调试](../debugger/getting-set-up-for-debugging.md)。
    - 请确保 [USB 客户端驱动程序所需的标头和库](headers-and-libraries-for-a-usb-client-driver.md) 可用。
    - 如果通过以太网网络写入主机和目标计算机上的内核模式驱动程序调试，则必须配置1394电缆、USB 2.0 或3.0 调试电缆或空调缆线电缆。
    - 如果写入用户模式驱动程序，则可在 Microsoft Visual Studio 环境中使用用户模式调试器。 开发人员应熟悉 [如何附加到进程或在调试器下启动进程](../debugger/debugging-a-user-mode-process-using-visual-studio.md)。

7. 编写您的第一个驱动程序。
    - [如何将第一个 USB 客户端驱动程序写入 (KMDF) ](tutorial--write-your-first-usb-client-driver--kmdf-.md)。
    - [如何将第一个 USB 客户端驱动程序写入 (UMDF) ](implement-driver-entry-for-a-usb-driver--umdf-.md)。
    - 使用 Visual Studio 2012 附带的 USB 模板，编写、生成和安装第一个 USB 客户端驱动程序。 开发人员应能够描述框架驱动程序、设备和队列对象，并了解框架如何与驱动程序通信。

8. 通过发送 USB 控件传输请求来扩展驱动程序。
    - 将标准控制请求和供应商命令发送到设备。 有关详细信息，请参阅 [如何发送 USB 控件传输](usb-control-transfer.md)。

9. 扩展你的驱动程序，使用 WDF USB i/o 目标对象执行 [USB 数据传输](usb-device-i-o.md)。
    - 扩展驱动程序以执行常见任务，如 [USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)中所述。

## <a name="community-resources-for-usb"></a>用于 USB 的社区资源

[Microsoft WINDOWS USB 核心团队博客](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/bg-p/MicrosoftUSBBlog) 查看 Microsoft USB 团队撰写的文章。 此博客重点介绍 Windows USB 驱动程序堆栈，该堆栈适用于 Windows 电脑中的各种 USB 主控制器和 USB 集线器。 适用于 USB 客户端驱动程序开发人员和 USB 硬件设计人员的资源，方便他们了解驱动程序堆栈实现、解决常见问题以及如何使用工具来收集跟踪和日志文件。

[OSR Online 列表](https://www.osronline.com/)  
由 [OSR Online](https://www.osronline.com/) 管理的讨论列表，适用于内核模式驱动程序开发人员。

[专注硬件开发的 Windows 开发人员中心](../dashboard/index.yml)  

[Windows 驱动程序工具包](../download-the-wdk.md)，通过 [Windows 硬件实验室工具包](/windows-hardware/test/hlk/)确保你的产品可靠且与 windows 兼容，并了解 [windows 驱动程序示例](../samples/index.md)。

## <a name="related-topics"></a>相关主题

[ (USB) 驱动程序的通用串行总线](../index.yml)  
[如何在 USB 设备的 UMDF 驱动程序中启用 USB 选择性挂起和系统唤醒](./selective-suspend-in-umdf-drivers.md)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)