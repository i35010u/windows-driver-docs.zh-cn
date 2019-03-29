---
Description: The goal of device testing is to test device usage against various hub scenarios and systems power states.
title: 测试与 MUTT 设备的 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40160a68101b12e60d5398c333c5c4e587201868
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561939"
---
# <a name="usb-device-testing-with-mutt-devices"></a>测试与 MUTT 设备的 USB 设备


设备测试的目标是要测试针对各种中心方案的设备使用情况和系统电源状态。 MUTT 包和 SuperMUTT 包设备可以提供一种方法来公开设备以连接/断开跨不同中心的方案，以及系统电源状态方案。 当分别附加到 USB 2.0 和 3.0 版集线器中 MUTT 包和 SuperMUTT 包的设备，则测试设备。

## <a name="usb-device-testing-prerequisites"></a>USB 设备测试先决条件


在提升的命令提示符处运行 MUTT 测试命令之前，请确保满足以下要求：

-   测试系统必须运行 Windows 8 的最新版本。
-   设置和配置 MUTT 设备并安装固件。 有关详细信息，请参阅[如何进行准备，测试系统运行的测试工具的 MUTT](mutt-testing-options.md)。

## <a name="suggested-device-tests"></a>建议的设备测试


-   USB IF 电气测试。 所有我们的测试都是协议和已设定焦点的状态。 请参阅[USB-如果符合性计划](http://www.usb.org/developers/compliance/)的电气测试的详细信息。
-   设备基本测试。 有关详细信息，请参阅[如何为 MUTT 设备运行 Visual Studio 中的说明测试](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)。
-   控制器 Windows 硬件认证工具包测试。 有关详细信息，请参阅[USB-如果证书验证测试 （控制器）](https://go.microsoft.com/fwlink/p/?linkid=316509)。
-   对于主机控制器，在部分中的 Windows 测试指南文档中找到的手动测试用例。

## <a name="topologies-for-testing-usb-devices"></a>用于测试 USB 设备的拓扑


请考虑以下待测试的 USB 设备的配置：

-   测试设备是 SuperMUTT 包的下一级。

    ![设备是 supermutt 包的下一级](images/fig13-topology-downstream-supermuttpack.png)

-   测试设备是 MUTT 包的下一级。

    ![设备是下游 mutt 包中](images/fig14-topology-downstream-muttpack.png)

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



