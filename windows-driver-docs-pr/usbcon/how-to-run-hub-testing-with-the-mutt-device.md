---
description: 中心测试的目标是从设备生成一组完整的可能的流量模式。 可以通过添加上游 SuperMUTT 包来测试断开连接的情况。
title: USB 中心测试与 MUTT 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ff73ca7994a7dd9a1e4ffe6a2811cb791b5d4a7
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969252"
---
# <a name="usb-hub-testing-with-mutt-devices"></a>USB 中心测试与 MUTT 设备


中心测试的目标是从设备生成一组完整的可能的流量模式。 可以通过添加上游 SuperMUTT 包来测试断开连接的情况。

## <a name="hub-testing-prerequisites"></a>中心测试先决条件


在提升的命令提示符下运行 MUTT test 命令之前，请确保满足以下要求：

-   测试系统必须运行最新版本的 Windows 8。
-   设置并配置 MUTT 设备并安装固件。 有关详细信息，请参阅 [如何准备测试系统以运行 MUTT 测试工具](mutt-testing-options.md)。

## <a name="recommended-hub-tests"></a>建议的中心测试


-   如果是电气测试，则为 USB。 所有测试都是以协议和状态为重点的。 有关电气测试的详细信息，请参阅 [USB-IF 合规性计划](https://www.usb.org/compliance) 。
-   在 MUTT 设备附带的设备连接到 USB 控制器的建议配置中时，MUTT 应力和传输测试。 **RunTest.bat** 同时运行压力测试和传输测试。 请参阅 [如何为 MUTT 设备运行压力和传输性能测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)。
-   设备基础测试。 有关详细信息，请参阅 [如何在 Visual Studio FOR MUTT 设备中运行 devfund 测试](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)。
-   控制器 Windows 硬件认证工具包测试。 有关详细信息，请参阅 [USB-IF 认证验证测试 (控制器) ](https://go.microsoft.com/fwlink/p/?linkid=316509)。
-   宿主控制器的手动测试用例，如部分的 Windows 测试指南文档中所示。

## <a name="recommended-topologies-for-hub-testing-with-mutt-devices"></a>使用 MUTT 设备进行中心测试的推荐拓扑


-   将 MUTT 设备附加到每个可用的下游端口。
-   将 Supermutt 附加到一半可用端口。 将 MUTT 设备连接到剩余端口。
-   在测试下将中心的 SuperMutt 包附加到上游端口，下游端口具有相同数量的 SuperMUTT 和 MUTT 设备，如下图所示：

    ![测试连接/断开连接](images/fig14-topology-connect-disconnect.png)

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



