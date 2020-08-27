---
description: 控制器测试的目标是从集线器和设备生成一组完整的可能的流量模式。
title: USB 主机控制器测试与 MUTT 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f200694a1e219ddaa59e157e560abf9a92b2df8
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968956"
---
# <a name="usb-host-controller-testing-with-mutt-devices"></a>USB 主机控制器测试与 MUTT 设备


控制器测试的目标是从集线器和设备生成一组完整的可能的流量模式。 这允许完全测试控制器及其固件的内部状态。 MUTT 设备可提供一种自动化方法来生成各种可能的协议方案，从而帮助进行测试。

## <a name="usb-host-controller-testing-prerequisites"></a>USB 主机控制器测试先决条件


在提升权限的命令提示符下运行 MUTT test 命令之前，请确保满足以下要求：

-   测试系统必须运行最新版本的 Windows 8。
-   设置并配置 MUTT 设备并安装固件。 有关详细信息，请参阅 [如何准备测试系统以运行 MUTT 测试工具](mutt-testing-options.md)。

## <a name="recommended-usb-host-controller-tests"></a>推荐的 USB 主机控制器测试


-   如果是电气测试，则为 USB。 所有测试都是以协议和状态为重点的。 有关电气测试的详细信息，请参阅 [USB-IF 合规性计划](https://www.usb.org/compliance) 。
-   在 MUTT 设备附带的设备连接到 USB 控制器的建议配置中时，MUTT 应力和传输测试。 **RunTest.bat** 同时运行压力测试和传输测试。 请参阅 [如何为 MUTT 设备运行压力和传输性能测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)。
-   SuperMUTT 性能测试。 请参阅 [如何运行超级 MUTT 性能测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md#supermutt-perf)。
-   设备基础测试。 有关详细信息，请参阅 [如何在 Visual Studio FOR MUTT 设备中运行 devfund 测试](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)。
-   控制器 Windows 硬件认证工具包测试。 有关详细信息，请参阅 [USB-IF 认证验证测试 (控制器) ](https://go.microsoft.com/fwlink/p/?linkid=316509)。
-   宿主控制器的手动测试用例，如部分的 Windows 测试指南文档中所示。

## <a name="topologies-for-usb-host-controller-testing-with-mutt-devices"></a>用于通过 MUTT 设备进行 USB 主机控制器测试的拓扑


对于受测的 xHCI 控制器，请考虑以下配置：

-   将 MUTT 设备附加到所有可用端口。
-   划分可用端口，使 SuperMUTT 和 MUTT Pack 设备数相等。 对于 MUTT 包，附加下游 MUTT 设备。
-   将 Supermutt 附加到一半可用端口。 将 SuperMUTT Pack 设备附加到剩余端口。 对于 SuperMUTT 包，附加下游 SuperMUTT 设备。
-   您可以使用复杂的拓扑。 例如，考虑一个具有四个端口的控制器。 下图显示了一个示例拓扑。

    ![示例 xhci 控制器拓扑](images/fig12-xhci-controller-topology.png)

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



