---
title: 测试通用传感器驱动程序
description: 本主题提供有关如何测试通用传感器驱动程序的建议。
ms.assetid: 46F50544-B130-4690-8047-6FBB6DD4749F
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 23e67056e3deebc85ce4f72149cda7cb8a95d3d4
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355973"
---
# <a name="test-your-universal-sensor-driver"></a>测试通用传感器驱动程序

本主题提供有关如何测试通用传感器驱动程序的建议。

## <a name="sensor-driver-specific-testing"></a>特定于传感器驱动程序的测试

成功 [将传感器连接到带 Cove 板](connect-your-sensor-to-the-sharks-cove-board.md)，并 [编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)后，可以使用以下工具测试/调试通用传感器驱动程序。

-   **MALT (Microsoft Ambent 轻型工具) ** <br/>可以使用 MALT 工具作为轻测试解决方案。 有关详细信息，请参阅 [构建轻型测试工具](testing-MALT-building-a-light-testing-tool.md)。

-   **SensorInfo 应用** <br/>如果要使用通用 Windows 平台 (UWP) 应用测试传感器驱动程序，则可以使用 [SensorInfo 应用](https://www.microsoft.com/store/appid/95015d9e-2116-44b8-9d3c-15c7b8753086)。 此应用将自动检测附加到 (或嵌入) 平台中的任何传感器，然后调用关联的驱动程序。 然后，该应用将显示它从传感器中读取的信息，并将该信息显示为移动波形。

-   **传感器诊断工具** <br/>如果只是想要监视数据检索、事件处理、报告间隔等，请在带 Cove 上安装此工具，以监视这些传感器值。 传感器诊断工具附带了 Windows 驱动程序工具包 (WDK) ，可在以下文件夹中找到： * &lt; 工具包根 &gt; \\ 工具 \\ &lt; 体系结构 &gt; \\sensordiagnostictool.exe*。 <br/><br/>例如，如果你的驱动程序开发计算机是基于 x64 的计算机，并且你将该 WDK 安装到了默认位置，则会在以下文件夹中找到传感器诊断工具：<br/><br/>*C： \\ Program Files (x86) \\ Windows 工具包 \\ 10 \\ 工具 \\ x64 \\sensordiagnostictool.exe* <br/><br/>**注意**  传感器诊断工具现已弃用，适用于 Windows 10。 对于所有传感器测试和诊断，请使用 Microsoft Store 中的 SensorInfo 应用。

## <a name="general-driver-testing"></a>常规驱动程序测试

如果要了解有关一般测试驱动程序的信息，请参阅以下资源。

-   **Visual Studio Kernel-Mode 调试，使用串行 over USB**
    <br/>如果希望在为传感器设置调试会话及其通用传感器驱动程序时使用 Visual Studio 的帮助，请使用此测试/调试选项。 有关详细信息，请参阅 [在 Visual Studio 中使用串口 OVER USB 设置 Kernel-Mode 调试](../debugger/setting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio.md)。
-   **手动设置 Kernel-Mode 调试，使用串连 over USB**
    <br/>如果要测试/调试通用传感器驱动程序，但不希望使用 Visual Studio 进行设置，则可以使用此选项。 有关如何执行此操作的说明，请参阅 [使用手动设置 Kernel-Mode 调试](/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)。
-   **WDK 驱动程序测试接口** 可以通过 Microsoft Visual Studio 使用 Windows 驱动程序工具包 (WDK) 驱动程序测试界面来测试驱动程序。 有关如何执行此操作的信息，请参阅 [测试驱动程序](../develop/testing-a-driver.md)。

有关如何监视跟踪提供程序的操作的信息，请参阅 [收集和解码 WPP 日志](collecting-and-decoding-wpp-logs.md)。