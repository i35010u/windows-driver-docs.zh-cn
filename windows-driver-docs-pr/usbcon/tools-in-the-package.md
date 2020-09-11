---
description: 设备测试的目的是针对各种集线器方案和系统电源状态测试设备使用情况。
title: USB 设备测试与 MUTT 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4c0485c4a08d278788428f32bf144a8f51627a5
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009849"
---
# <a name="usb-device-testing-with-mutt-devices"></a>USB 设备测试与 MUTT 设备


设备测试的目的是针对各种集线器方案和系统电源状态测试设备使用情况。 MUTT Pack 和 SuperMUTT Pack 设备可提供一种方法来公开设备，以便跨不同的集线器和系统电源状态方案连接/断开连接。 如果设备已分别连接到 MUTT Pack 和 SuperMUTT Pack 设备中的 USB 2.0 和3.0 集线器，请测试该设备。

## <a name="usb-device-testing-prerequisites"></a>USB 设备测试先决条件


在提升的命令提示符下运行 MUTT test 命令之前，请确保满足以下要求：

-   测试系统必须运行最新版本的 Windows 8。
-   设置并配置 MUTT 设备并安装固件。 有关详细信息，请参阅 [如何准备测试系统以运行 MUTT 测试工具](mutt-testing-options.md)。

## <a name="suggested-device-tests"></a>建议的设备测试


-   如果是电气测试，则为 USB。 所有测试都是以协议和状态为重点的。 有关电气测试的详细信息，请参阅 [USB-IF 合规性计划](https://www.usb.org/compliance) 。
-   设备基础测试。 有关详细信息，请参阅 [如何在 Visual Studio FOR MUTT 设备中运行 devfund 测试](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)。
-   控制器 Windows 硬件认证工具包测试。 有关详细信息，请参阅 [USB-IF 认证验证测试 (控制器) ](https://go.microsoft.com/fwlink/p/?linkid=316509)。
-   宿主控制器的手动测试用例，如部分的 Windows 测试指南文档中所示。

## <a name="topologies-for-testing-usb-devices"></a>用于测试 USB 设备的拓扑


对于受测的 USB 设备，请考虑以下配置：

-   测试设备是 SuperMUTT Pack 的下游。

    ![设备是 supermutt pack 的下游](images/fig13-topology-downstream-supermuttpack.png)

-   测试设备是 MUTT Pack 的下游。

    ![设备从 mutt 包下游](images/fig14-topology-downstream-muttpack.png)

## <a name="related-topics"></a>相关主题
[USB](../index.yml)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)