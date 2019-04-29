---
Description: 测试控制器的目标是从中心和设备生成一组完整的可能的通信模式。
title: USB 主控制器使用 MUTT 设备进行测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb66bf48481da17e45a06d979797a61364c6957
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366049"
---
# <a name="usb-host-controller-testing-with-mutt-devices"></a>USB 主控制器使用 MUTT 设备进行测试


测试控制器的目标是从中心和设备生成一组完整的可能的通信模式。 这样，控制器和其固件要完全测试的内部状态。 MUTT 设备提供自动的方法，以生成各种可能的协议方案，可帮助测试。

## <a name="usb-host-controller-testing-prerequisites"></a>USB 主机控制器测试先决条件


在提升的命令提示符运行 MUTT 测试命令之前，请确保满足以下要求：

-   测试系统必须运行 Windows 8 的最新版本。
-   设置和配置 MUTT 设备并安装固件。 有关详细信息，请参阅[如何进行准备，测试系统运行的测试工具的 MUTT](mutt-testing-options.md)。

## <a name="recommended-usb-host-controller-tests"></a>推荐的 USB 主机控制器测试


-   USB IF 电气测试。 所有我们的测试都是协议和已设定焦点的状态。 请参阅[USB-如果符合性计划](http://www.usb.org/developers/compliance/)的电气测试的详细信息。
-   MUTT 压力和传输测试包含在 MUTT 软件包 MUTT 设备连接的 USB 控制器建议的配置中。 **RunTest.bat**运行压力和传输的测试。 请参阅[如何运行压力和传输 MUTT 设备的性能测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)。
-   SuperMUTT 性能测试。 请参阅[如何运行超级 MUTT 性能测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md#supermutt-perf)。
-   设备基本测试。 有关详细信息，请参阅[如何为 MUTT 设备运行 Visual Studio 中的说明测试](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)。
-   控制器 Windows 硬件认证工具包测试。 有关详细信息，请参阅[USB-如果证书验证测试 （控制器）](https://go.microsoft.com/fwlink/p/?linkid=316509)。
-   对于主机控制器，在部分中的 Windows 测试指南文档中找到的手动测试用例。

## <a name="topologies-for-usb-host-controller-testing-with-mutt-devices"></a>USB 主控制器使用 MUTT 设备进行测试的拓扑


请考虑待测试的 xHCI 控制器的以下配置：

-   将 MUTT 设备附加到所有可用端口。
-   划分可用端口，以便 SuperMUTT 和 MUTT 包设备的数目相同。 MUTT 包将附加下游 MUTT 设备。
-   将 Supermutt 附加到一半的可用端口。 将 SuperMUTT 包设备附加到剩余的端口。 SuperMUTT 包将附加下游 SuperMUTT 设备。
-   可以具有的复杂拓扑。 例如，考虑具有四个端口的控制器。 下图显示了示例拓扑。

    ![xhci 控制器的示例拓扑](images/fig12-xhci-controller-topology.png)

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



