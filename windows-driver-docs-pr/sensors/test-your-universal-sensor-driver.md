---
title: 测试通用传感器驱动程序
description: 本主题提供有关如何测试您的通用传感器驱动程序的建议。
ms.assetid: 46F50544-B130-4690-8047-6FBB6DD4749F
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d0b2c481efb93022e0bd2ad75cce630f2f1b108
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548106"
---
# <a name="test-your-universal-sensor-driver"></a>测试通用传感器驱动程序

本主题提供有关如何测试您的通用传感器驱动程序的建议。

## <a name="sensor-driver-specific-testing"></a>传感器特定于驱动程序的测试

后成功[传感器连接到 Shark Cove 板](connect-your-sensor-to-the-sharks-cove-board.md)，并且您[编写和部署通用传感器驱动程序](write-and-deploy-your-universal-sensor-driver.md)，以下工具可用来进行测试/调试通用传感器驱动程序。

-   **MALT （Microsoft Ambent Light 工具）** <br/>您可以使用 MALT 工具作为测试解决方案的光。 有关详细信息，请参阅[构建 Light 测试工具](testing-MALT-building-a-light-testing-tool.md)。

-   **SensorInfo 应用** <br/>如果你想要使用的通用 Windows 平台 (UWP) 应用程序测试传感器驱动程序，则可以使用[SensorInfo 应用](http://apps.microsoft.com/windows/app/95015d9e-2116-44b8-9d3c-15c7b8753086?ocid=Apps_Search_WOL_en-us_search-main_search-results-from_search-sensorinfo_image_sensorinfo)。 此应用将自动检测任何传感器附加到 （或嵌入在） 平台上，然后调用关联的驱动程序。 然后，应用将显示它从传感器读取的信息，并作为移动波形中显示的信息。

-   **传感器诊断工具** <br/>如果只是想要监视数据检索，事件处理报表的时间间隔等，然后在 Shark Cove 来监视这些传感器值上安装此工具。 传感器诊断工具附带 Windows 驱动程序工具包 (WDK)，并可在以下文件夹中找到：*&lt;工具包根&gt;\\工具\\&lt;体系结构&gt;\\sensordiagnostictool.exe*。 <br/><br/>例如，如果驱动程序开发计算机是基于 x64 的计算机，并在默认位置安装了 WDK，那么您将找到传感器诊断工具在以下文件夹中：<br/><br/>*C:\\程序文件 (x86)\\Windows 工具包\\10\\工具\\x64\\sensordiagnostictool.exe* <br/><br/>**请注意**  传感器诊断工具现在不推荐使用适用于 Windows 10。 请 SensorInfo 应用从 Microsoft Store 中，使用的所有传感器测试和诊断。

## <a name="general-driver-testing"></a>通用驱动程序测试

如果你想要了解有关在常规，请参阅以下资源测试驱动程序的信息。

-   **Visual Studio 内核模式调试，通过 USB 使用序列**
    <br/>使用此测试/调试选项时，如果想要设置您的传感器和其通用传感器驱动程序的调试会话中的 Visual Studio 的帮助。 有关详细信息，请参阅[设置内核模式调试使用通过 Visual Studio 中的 USB 串行](https://msdn.microsoft.com/library/windows/hardware/dn745913.aspx)。
-   **手动设置内核模式调试中，使用通过 USB 串行**
    <br/>如果想要测试/调试通用传感器驱动程序，但不想要用于执行安装程序中使用 Visual Studio，可以使用此选项。 有关如何执行此操作的说明，请参阅[设置内核模式调试使用通过 USB 手动序列](https://msdn.microsoft.com/library/windows/hardware/dn745914.aspx)。
-   **WDK 驱动程序测试接口**可以使用 Windows 驱动程序工具包 (WDK) 驱动程序测试接口通过 Microsoft Visual Studio 中，若要测试的驱动程序。 有关如何执行此操作的信息，请参阅[测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)。

有关如何监视跟踪提供程序的运行状况的信息，请参阅[日志收集和解码 WPP](collecting-and-decoding-wpp-logs.md)。








