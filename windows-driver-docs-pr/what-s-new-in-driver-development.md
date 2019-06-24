---
title: 驱动程序开发中的新增功能
description: 本部分介绍 Windows 10 中驱动程序开发的新增功能。
ms.assetid: 5502AAF9-2400-4338-A646-C746B29F9A44
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f60441488e80443a78e6114285601c6cfe1c096b
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "66813591"
---
# <a name="top"></a>驱动程序开发中的新增功能

本部分提供有关 Windows 10 中 Windows 驱动程序开发的新增功能和更新的信息。

下面列出了 Windows 10 中驱动程序开发的新增功能亮点。

* [Windows 10 版本 1903 WDK 支持 Visual Studio 2019](#wdk-supports-visual-studio-2019)
* [Windows 硬件开发人员中心仪表板](#windows-hardware-dev-center-dashboard)
* [开放发布](#open-publishing)
* [Windows 调试工具](#debugging-tools-for-windows)
* [设备和驱动程序安装](#device-and-driver-installation)
* [驱动程序验证程序](#driver-verifier)
* [Windows 驱动程序框架](#windows-driver-frameworks-wdf)
* [通用 Windows 驱动程序](#universal-windows-drivers)
* [Windows 兼容的硬件开发板](#windows-compatible-hardware-development-boards)
* [电源管理框架](#power-management-framework)
* [系统提供的驱动程序接口](#system-supplied-driver-interfaces)
* [WPP 软件跟踪](#wpp-software-tracing)

下表按驱动程序技术和版本列出了 Windows 10 中的功能更新。

| 驱动程序  |[1903](#whats-new-in-windows-10-version-1903-latest)| [1809](#whats-new-in-windows-10-version-1809) |   [1803](#whats-new-in-windows-10-version-1803)    | [1709](#whats-new-in-windows-10-version-1709) |  [1703](#whats-new-in-windows-10-version-1703)  | [1607](#whats-new-in-windows-10-version-1607) |  [1507](#whats-new-in-windows-10-version-1507)  |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Audio  |  [![详细信息](checkmark.png)](#audio-1903) |      [![详细信息](checkmark.png)](#audio-1809)       |      [![详细信息](checkmark.png)](#audio-1803)      |         [![详细信息](checkmark.png)](#audio-1709)          |      [![详细信息](checkmark.png)](#audio-1703)      |      [![详细信息](checkmark.png)](#audio-1607)      |                   ![不可用](minus.png)                   |
|               ACPI         |   ![不可用](minus.png)    |             ![不可用](minus.png)              |      [![详细信息](checkmark.png)](#acpi-1803)       |          [![详细信息](checkmark.png)](#acpi-1709)          |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|             生物识别    |     ![不可用](minus.png)   |             ![不可用](minus.png)              |            ![不可用](minus.png)             |       [![详细信息](checkmark.png)](#biometric-1709)        |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|             蓝牙     |   ![不可用](minus.png)     |     [![详细信息](checkmark.png)](#bluetooth-1809)     |    [![详细信息](checkmark.png)](#bluetooth-1803)    |                ![不可用](minus.png)                |    [![详细信息](checkmark.png)](#bluetooth-1703)    |          ![不可用](minus.png)          |             [![详细信息](checkmark.png)](#bluetooth-1507)             |
|          总线和端口          |   ![不可用](minus.png)   |       ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |          [![详细信息](checkmark.png)](#buses-and-ports)          |
|              相机       |    [![详细信息](checkmark.png)](#camera-1903)    |             ![不可用](minus.png)              |     [![详细信息](checkmark.png)](#camera-1803)      |                ![不可用](minus.png)                |     [![详细信息](checkmark.png)](#camera-1703)      |   [![详细信息](checkmark.png)](#camera-1607)   |            [![详细信息](checkmark.png)](#camera-1507)            |
|             手机网络              |   ![不可用](minus.png)   |       ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |             [![详细信息](checkmark.png)](#cellular)              |
|              显示          |  [![详细信息](checkmark.png)](#display-1903) |      [![详细信息](checkmark.png)](#display-1809)      |     [![详细信息](checkmark.png)](#display-1803)     |        [![详细信息](checkmark.png)](#display-1709)         |            ![不可用](minus.png)             |          ![不可用](minus.png)          |              [![详细信息](checkmark.png)](#display-1507)              |
|          驱动程序安全性      |  ![不可用](minus.png)  |             ![不可用](minus.png)              |    [![详细信息](checkmark.png)](#security-1803)     |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |              ![不可用](minus.png)              |
|      硬件通知    | ![不可用](minus.png)  |             ![不可用](minus.png)              |            ![不可用](minus.png)             | [![详细信息](checkmark.png)](#hardware-notifications-1709) |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|   人体学接口设备 (HID)    |    ![不可用](minus.png)    |     ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |      [![详细信息](checkmark.png)](#human-interface-device)       |
|              内核          |   ![不可用](minus.png)  |      [![详细信息](checkmark.png)](#kernel-1809)       |     [![详细信息](checkmark.png)](#kernel-1803)      |         [![详细信息](checkmark.png)](#kernel-1709)         |     [![详细信息](checkmark.png)](#kernel-1703)      |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|             位置       |   ![不可用](minus.png)    |             ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |  [![详细信息](checkmark.png)](#location-1607)  |           [![详细信息](checkmark.png)](#location-1507)           |
|         移动宽带    |    [![详细信息](checkmark.png)](#mobilebroadband-1903)  |  [![详细信息](checkmark.png)](#mobilebroadband-1809)  | [![详细信息](checkmark.png)](#mobilebroadband-1803) |    [![详细信息](checkmark.png)](#mobilebroadband-1709)     | [![详细信息](checkmark.png)](#mobilebroadband-1703) |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|     近场通信      |    ![不可用](minus.png)     |    ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |     [![详细信息](checkmark.png)](#near-field-communication)      |
|            网络     |    [![详细信息](checkmark.png)](#networking-1903)    |    [![详细信息](checkmark.png)](#networking-1809)     |   [![详细信息](checkmark.png)](#networking-1803)    |       [![详细信息](checkmark.png)](#networking-1709)       |   [![详细信息](checkmark.png)](#networking-1703)    |          ![不可用](minus.png)          |          [![详细信息](checkmark.png)](#networking-1507)          |
|                POS          |   ![不可用](minus.png)   |             ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |       [![详细信息](checkmark.png)](#pos-1703)       |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|                PCI        |    ![不可用](minus.png)    |             ![不可用](minus.png)              |       [![详细信息](checkmark.png)](#pci-1803)       |          [![详细信息](checkmark.png)](#pci-1709)           |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|               Print     |      [![详细信息](checkmark.png)](#print-1903)    |             ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |   [![详细信息](checkmark.png)](#print-1607)    |            [![详细信息](checkmark.png)](#print-1507)             |
|      脉宽调制       |   ![不可用](minus.png)  |        ![不可用](minus.png)              |            ![不可用](minus.png)             |          [![详细信息](checkmark.png)](#pwm-1709)           |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|              传感器        |  [![详细信息](checkmark.png)](#sensors-1903)    |      [![详细信息](checkmark.png)](#sensors-1809)      |     [![详细信息](checkmark.png)](#sensors-1803)     |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|            智能卡     |    ![不可用](minus.png)    |             ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |            [![详细信息](checkmark.png)](#smart-card)             |
|              存储         |    [![详细信息](checkmark.png)](#storage-1903)  |             ![不可用](minus.png)              |            ![不可用](minus.png)             |        [![详细信息](checkmark.png)](#storage-1709)         |            ![不可用](minus.png)             |          ![不可用](minus.png)          |              [![详细信息](checkmark.png)](#storage-1507)              |
| 系统提供的驱动程序接口 |   ![不可用](minus.png)   |      ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          | [![详细信息](checkmark.png)](#system-supplied-driver-interfaces) |
|                USB                |  ![不可用](minus.png) |     [![详细信息](checkmark.png)](#usb-1809)        |       [![详细信息](checkmark.png)](#usb-1803)       |          [![详细信息](checkmark.png)](#usb-1709)           |       [![详细信息](checkmark.png)](#usb-1703)       |          ![不可用](minus.png)          |                [![详细信息](checkmark.png)](#usb-1507)                |
|               WI-FI           |  [![详细信息](checkmark.png)](#wifi-1903)  |       [![详细信息](checkmark.png)](#wifi-1809)        |      [![详细信息](checkmark.png)](#wifi-1803)       |                ![不可用](minus.png)                |            ![不可用](minus.png)             |          ![不可用](minus.png)          |                   ![不可用](minus.png)                   |
|               WLAN         |    ![不可用](minus.png)   |             ![不可用](minus.png)              |            ![不可用](minus.png)             |                ![不可用](minus.png)                |            ![不可用](minus.png)             |    [![详细信息](checkmark.png)](#wlan-1607)    |             [![详细信息](checkmark.png)](#wlan-1507)             |

## <a name="whats-new-in-driver-development-for-windows-10"></a>Windows 10 驱动程序开发中的新增功能

[返回页首](#top)

本部分提供 Windows 10 中驱动程序开发的新增功能亮点。

### <a name="wdk-supports-visual-studio-2019"></a>WDK 支持 Visual Studio 2019。

适用于 Windows 10 版本 1903 的 Windows 驱动程序工具包 (WDK) 已更新，可以支持先前已[宣布](https://social.msdn.microsoft.com/Forums/en-US/b116571d-d5b2-4c1c-a43e-4b57171c8c41/windows-driver-kit-wdk-to-support-visual-studio-2019?forum=wdk)推出的 Visual Studio 2019。 但是，此 WDK 版本与 Visual Studio 2017 不兼容，开发人员可以通过旧版 WDK（在[此处](https://docs.microsoft.com/en-us/windows-hardware/drivers/other-wdk-downloads)可以找到版本 1709 至 1809）继续使用 Visual Studio 2017。 若要了解 Visual Studio 2019 的新增功能，请查看[此处](https://docs.microsoft.com/en-us/visualstudio/releases/2019/release-notes#whats-new-in-visual-studio-2019)的信息。

下面是 Windows 驱动程序开发人员在 Visual Studio 2019 中可以看到的几处显著更改。

#### <a name="wdk-gui-driver-menu-moved"></a>WDK GUI 驱动程序菜单已移动

在 Visual Studio 2019 中，WDK 驱动程序菜单已移到“扩展”菜单下，如下所示。

![Visual Studio 2019 菜单的屏幕截图](images/vs-2019-driver-menu.png)

Visual Studio 2017 中的 WDK 驱动程序菜单位于顶部菜单选项中，如下所示。

![Visual Studio 2017 菜单的屏幕截图](images/vs-2017-menu.png)

#### <a name="driver-templates-discoverability"></a>驱动程序模板可发现性

在 Visual Studio 2019 中，可在“项目类型”>“驱动程序”下发现 WDK 驱动程序模板。 驱动程序项目类型将显示在 Visual Studio 2019 的第一个官方更新版本中。 到时，可以通过在搜索菜单中进行搜索，来发现驱动程序模板。

![Visual Studio 2019 驱动程序模板的屏幕截图](images/vs-2019-driver-template.png)

以前，在 Visual Studio 2017 中，可以在“新建项目”>“Visual C++”>“Windows 驱动程序”下找到 WDK 驱动程序模板，如下所示。

![Visual Studio 2017 驱动程序模板的屏幕截图](images/vs-2017-driver-template.png)

### <a name="windows-hardware-dev-center-dashboard"></a>Windows 硬件开发人员中心仪表板

在 Windows 10 版本 1809 中，在[硬件 API](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-api) 方面，我们为开发人员、IHV 和 OEM 添加了新的和改进的功能，用于跟踪驱动程序包以及将其提交到 Windows 硬件仪表板。

使用发货标签 REST API 可以像分发驱动程序一样创建和管理发货标签。

* [管理发货标签](https://docs.microsoft.com/windows-hardware/drivers/dashboard/manage-shipping-labels)
* [获取发货标签数据](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-shipping-labels)

使用异步自定义报告方法可以访问驱动程序错误和 OEM 硬件错误的报告数据。 可根据需要定义报告模板、设置计划，系统会定期向你传送数据。

* [计划自定义报告以获取驱动程序故障详细信息](https://docs.microsoft.com/windows-hardware/drivers/dashboard/schedule-custom-reports-for-driver-failure-details)

### <a name="open-publishing"></a>开放发布

我们正在努力使文档与社区活动更加相关。 在 Windows 驱动程序文档的许多页面上，你可以直接提出更改建议。 在页面的右上角可以找到“参与”按钮。  它如下所示：

![“参与”按钮的屏幕截图](contribute-button.png)

单击“参与”时，会转到 [GitHub 存储库](https://github.com/MicrosoftDocs/windows-driver-docs)中相关主题的 Markdown 源文件。  在此处可以单击“编辑”并提出更改建议。 

有关更多详细信息，请参阅存储库中的 [CONTRIBUTING.md](https://github.com/MicrosoftDocs/windows-driver-docs/blob/staging/CONTRIBUTING.md)。 感谢你花费时间来改进文档！

### <a name="debugging-tools-for-windows"></a>Windows 调试工具

本部分介绍 Windows 调试工具中的更改。

#### <a name="debugging-in-windows-10-version-1903"></a>Windows 10 版本 1903 中的调试

* 添加了新的停止代码，以便更好地跟踪 Windows 操作系统中的独特故障类型。 此外，还补充并更新了大量现有的 bug 检查主题。 有关详细信息，请参阅 [Bug 检查代码参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)。

* 更新了 KDNET 主题（例如，在新文章[自动设置 KDNET 网络内核调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)中）以提高易用性

* 更新了 IP V6 KDNET 支持。

* 新的 [JavaScript 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting)主题

#### <a name="debugging-in-windows-10-version-1809"></a>Windows 10 版本 1809 中的调试

* **新的调试器数据模型 API** – 现已推出一个新的面向对象的调试器数据模型接口，该接口可使用 dbgmodel.h 标头支持调试器自动化。 调试器数据模型是一种可扩展的对象模型，它能够让新调试器扩展（包括 JavaScript、NatVis 和 C++ 中的扩展）使用来自调试器的信息并生成可从调试器及其他扩展访问的信息。 可以在调试器的 dx 表达式计算器中以及从 JavaScript 扩展或 C++ 扩展访问写入到数据模型 API 的构造。 文档位置：[调试器数据模型 C++ 接口概述](debugger/data-model-cpp-overview.md)和 [dbgmodel.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/) 标头参考主题。

* **IPv6** - 我们将在 KDNET 中添加对 IPv6 的支持。 为了给 IPv6 所需的较大标头留出空间，我们减少了数据包的有效负载大小。 因此，我们将会声明 KDNET 协议的新版本，使运行最新版调试器的主机电脑可用于调试仅支持 IPv4 的目标电脑。 [https://aka.ms/windbgpreview](https://aka.ms/windbgpreview) 上提供了支持 IPv6 的 WinDbg 预览版。 请关注“Windows 调试工具”博客来了解有关 KDNET IPv6 支持的最新信息，并参阅[手动设置 KDNET 网络内核调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)了解更多详细信息。

#### <a name="debugging-in-windows-10-version-1803"></a>Windows 10 版本 1803 中的调试

[WinDbg 预览版时光穿越调试 (TTD) 动手实验](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-walkthrough) - 此实验使用一个存在代码缺陷的示例小程序介绍时光穿越调试 (TTD)。 TTD 用于调试、识别问题及分析其根本原因。

#### <a name="debugging-in-windows-10-version-1709"></a>Windows 10 版本 1709 中的调试

下面是 Windows 10 版本 1709 中调试器的新内容集列表：

* [使用 WinDbg 预览版进行调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-windbg-preview) - 预览下一代调试器。
* [时光穿越调试 - 概述](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-overview) - 记录和重放过程的执行。

#### <a name="debugging-in-windows-10-version-1703"></a>Windows 10 版本 1703 中的调试

下表显示了 Windows 10 版本 1703 中调试器的更改：

| 新主题 | 更新的主题 |
| --- | --- |
| [JavaScript 调试器脚本](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting) | [dtx（显示类型 - 扩展的调试器对象模型信息）](https://docs.microsoft.com/windows-hardware/drivers/debugger/dtx--display-type---extended-debugger-object-model-information-)命令 |
| [Bug 检查代码参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)中 40 个未经阐述的停止代码 | 对[配置 tools.ini](https://docs.microsoft.com/windows-hardware/drivers/debugger/configuring-tools-ini) 主题做了更新，在命令行调试器的 tools.ini 文件中添加了更多选项 |
| [!ioctldecode 命令](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ioctldecode) | [dx（显示调试器对象模型扩展）](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)命令中的新命令功能 |

#### <a name="debugging-in-windows-10-version-1607"></a>Windows 10 版本 1607 中的调试

在 Windows 10 版本 1607 中，调试器的更改包括有关[使用 WinDbg 调试 UWP 应用](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-a-uwp-app-using-windbg)的新主题，并更新了 [Bug 检查代码参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)中 30 个查看次数最多的开发人员 Bug 检查主题。

#### <a name="debugging-in-windows-10-version-1507"></a>Windows 10 版本 1507 中的调试

下面是 Windows 10 版本 1507 中 Windows 调试器的新命令列表：

* [**dx（显示 NatVis 表达式）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)- 使用 NatVis 扩展模型显示对象信息的新调试器命令。
* [ **.settings**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-settings--set-debug-settings-) - 在 Debugger.Settings 命名空间中设置、修改、显示、加载和保存设置的新命令。

### <a name="device-and-driver-installation"></a>设备和驱动程序安装

在 Windows 10 版本 1809 中添加了以下内容：

* [INF AddEventProvider 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addeventprovider-directive)
* [INF DDInstall.Events 节](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-events-section)

更新了以下内容：

* [提前启动反恶意软件的要求](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-requirements)
* [内核模式代码签名要求](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-requirements--windows-vista-and-later-)

### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序包含以下技术的新驱动程序验证规则：

* 新的[音频驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-audio-drivers)
* 新的 [AVStream 驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-avstream-drivers)
* 四个新的 [KMDF 驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-kmdf-drivers)
* 三个新的 [NDIS 驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-ndis-drivers)
* 版本 1703 中添加了新的 [Nullcheck 规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/nullcheck) 

### <a name="windows-driver-frameworks-wdf"></a>Windows 驱动程序框架 (WDF)

#### <a name="wdf-in-windows-10-version-1903"></a>Windows 10 版本 1903 中的 WDF

在 Windows 10 版本 1903 中，Windows 驱动程序框架 (WDF) 包括内核模式驱动程序框架 (KMDF) 版本 1.29 和用户模式驱动程序框架 (UMDF) 版本 2.29。

有关这些框架版本的功能的信息，请参阅 [Windows 10 中 WDF 驱动程序的新增功能](https://docs.microsoft.com/windows-hardware/drivers/wdf/)。
若要了解在旧版 WDF 中添加了哪些功能，请参阅 [KMDF 版本历史记录](https://docs.microsoft.com/windows-hardware/drivers/wdf/kmdf-version-history)和 [UMDF 版本历史记录](https://docs.microsoft.com/windows-hardware/drivers/wdf/umdf-version-history)。

### <a name="universal-windows-drivers"></a>通用 Windows 驱动程序

本部分介绍 Windows 10 中通用 Windows 驱动程序的新增功能和已更新的功能。

[返回页首](#top)

#### <a name="universal-drivers-in-windows-10-version-1809"></a>Windows 10 版本 1809 中的通用驱动程序

从 Windows 10 版本 1809 开始，Windows 支持灵活链接，可让你使用单个二进制文件来以 OneCore 和桌面 SKU 为目标。
若要启用灵活链接，请使用以下新的 SDK API：

* [IsApiSetImplemented](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented)

此现有主题已得到增强，其中介绍了如何使用灵活链接来满足 [DCHU 驱动程序设计原则](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers#design-principles)的 U 要求：

* [针对 OneCore 生成](https://docs.microsoft.com/windows-hardware/drivers/develop/building-for-onecore)

#### <a name="universal-drivers-in-windows-10-version-1803"></a>Windows 10 版本 1803 中的通用驱动程序

在[通用驱动程序入门](develop/getting-started-with-universal-drivers.md)中查看有关通用驱动程序的最新建议。

#### <a name="universal-drivers-in-windows-10-version-1709"></a>Windows 10 版本 1709 中的通用驱动程序

下面是 Windows 10 版本 1709 中通用驱动程序的新增功能列表：

* [使用 Windows 更新来更新设备固件](https://docs.microsoft.com/windows-hardware/drivers/install/updating-device-firmware-using-windows-update) - 介绍如何使用 Windows 更新 (WU) 服务更新可移动设备或机箱内部设备的固件。
* [Reg2inf](https://docs.microsoft.com/windows-hardware/drivers/devtest/reg2inf) - 驱动程序包 INF 注册表转换工具 (reg2inf.exe) 可将注册表项及其值或者用于实现 DLL RegisterServer 例程的 COM.dll 转换成一组 INF AddReg 指令。 这些指令包含在驱动程序包 INF 文件中。

下面是 Windows 10 版本 1709 中通用驱动程序的更新列表：

* [通用驱动程序方案](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios)包含新的 COM 组件示例
* [INF AddComponent 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addcomponent-directive)
* [使用扩展 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)
* [使用组件 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)

#### <a name="universal-drivers-in-windows-10"></a>Windows 10 中的通用驱动程序

从 Windows 10 开始，可以编写单个适用于基于 OneCoreUAP 的 Windows 版本的驱动程序。这些版本包括 Windows 10 桌面版（家庭版、专业版、企业版和教育版）、Windows 10 移动版和 Windows 10 IoT 核心版（IoT 核心版），等等。 此类驱动程序称为通用 Windows 驱动程序。 通用 Windows 驱动程序调用适用于 Windows 驱动程序的一部分接口。 有关如何生成、安装、部署和调试适用于 Windows 10 的通用 Windows 驱动程序的信息，请参阅[通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)。

使用 Microsoft Visual Studio 2015 生成通用 Windows 驱动程序时，Visual Studio 会自动检查驱动程序调用的 API 是否对通用 Windows 驱动程序有效。 还可以使用 ApiValidator.exe 作为独立工具来执行此任务。 ApiValidator.exe 工具是适用于 Windows 10 的 Windows 驱动程序工具包 (WDK) 的一部分。 有关信息，请参阅[验证通用 Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/validating-universal-drivers)。

通用 Windows 驱动程序还需要一种特殊类型的 INF 文件，称为“通用 INF”。  通用 INF 可以使用适用于传统 INF 文件的一部分指令和节。 有关详细信息，请参阅[使用通用 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)。 若要了解哪些节和指令适用，请参阅 [INF 文件节和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。

准备就绪后，请使用 [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif) 工具测试驱动程序的 INF 文件。 除了报告 INF 语法问题以外，该工具还会报告该 INF 文件是否适用于通用 Windows 驱动程序。

你还可以查找有关可从通用 Windows 驱动程序调用的 API 的信息。 此信息位于驱动程序参考页底部的“要求”块中。

例如，会看到如下所示的列表，其中告知给定的 DDI 是否为“通用”。 

![目标平台在“要求”块中设置为“通用”](targetplatform.png)

有关详细信息，请参阅[驱动程序参考页上的目标平台](https://docs.microsoft.com/windows-hardware/drivers/develop/windows-10-editions-for-universal-drivers)。

### <a name="windows-compatible-hardware-development-boards"></a>Windows 兼容的硬件开发板

现在，有更多的经济型开发板（例如 Raspberry Pi 2）支持 Windows。 加入我们的前期采用者社区，即可在该开发板上加载 Windows。 有关详细信息，请参阅 [Windows 兼容的硬件开发板](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/windows-compatible-hardware-development-boards)。

### <a name="power-management-framework"></a>电源管理框架

电源管理框架 (PoFx) 可让驱动程序为设备中的各个组件单独定义一个或多个可调整的性能状态集。 驱动程序可以使用性能状态来限制组件的工作负荷，以提供刚好足够的性能来满足工作负荷的当前需求。 有关详细信息，请参阅[组件级性能状态管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-performance-management)。

Windows 10 版本 1903 支持[定向电源管理框架 (DFx)](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework)。  相关的参考文档包括：

* [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)
* [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
* [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)
* [PoFxCompleteDirectedPowerDown](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedirectedpowerdown) 函数

有关 DFx 测试的信息，请参阅以下页：

* [定向 FX 单一设备测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
* [定向 FX 系统验证测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
* [PwrTest DirectedFx 方案](devtest/pwrtest-directedfx-scenario.md)

### <a name="wpp-software-tracing"></a>WPP 软件跟踪

[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)引入了新的功能：*即时跟踪记录器*。 如果驱动程序启用了 WPP 跟踪和 WPP 记录器，则会自动启用跟踪日志记录，你无需启动或停止跟踪会话即可轻松查看消息。 若要对日志进行更细微的控制，WPP 记录器允许 KMDF 驱动程序创建和管理自定义缓冲区。

* [用于日志跟踪的 WPP 记录器](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)
* [WppRecorderLogGetDefault](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-imp_wpprecorderloggetdefault)
* [WppRecorderLogCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)（仅限 KMDF）
* [WppRecorderDumpLiveDriverData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

## <a name="whats-new-in-windows-10-version-1903-latest"></a>Windows 10 版本 1903（最新版）中的新增功能

本部分介绍 Windows 10 版本 1903（Windows 10 2019 年 4 月更新）中驱动程序开发的新增功能和更新。

[返回页首](#top)

### <a name="audio-1903"></a>音频

下面是 Windows 10 版本 1903 中新的和更新的音频功能列表：

* 有关在新的 [eventdetectoroemadapter.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/eventdetectoroemadapter/) 标头中用于语音激活的音频 OEM 适配器的新参考主题。
* 新的远场音频信息： 
    * [PKEY_Devices_AudioDevice_Microphone_IsFarField](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-devices-audiodevice-microphone-isfarfield)
    * [KSPROPSETID_InterleavedAudio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-interleavedaudio)
    * [KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION](https://review.docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-interleavedaudio-formatinformation)
    
* [USB 音频 2.0 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/usb-2-0-audio-drivers)中的新插孔说明信息。

### <a name="camera-1903"></a>相机

在 Windows 10 版本 1903 中添加的新相机驱动程序文档和功能包括：

* 新的[红外闪光灯](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-irtorchmode)扩展属性控件，可以设置红外相机的红外闪光灯功率级和占空比。
* 新的 [KSCATEGORY_NETWORK_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-network-camera) 设备。
* 为以下控件选择器新编和更新了 [USB 视频类 (UVC) 1.5 扩展](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)文档：
  * MSXU_CONTROL_FACE_AUTHENTICATION
  * MSXU_CONTROL_METADATA
  * MSUX_CONTROL_IR_TORCH

### <a name="display-1903"></a>显示

Windows 10 版本 1903 中的显示驱动程序开发的更新包括：

* **超级湿墨**：添加了新的 DDI 以实现前端缓冲渲染。 请参阅 [D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags) 和 [PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation)。

* **可变速率着色**：在不同的渲染图像中以不同的速率分配渲染性能/算力。 请参阅 [PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062) 和 [D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062)。

* **收集诊断信息**：允许 OS 从包括渲染和显示功能的图形适配器的驱动程序中收集专用数据。 请参阅 [DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo)。

* **后台处理**：允许用户模式驱动程序表达所需的线程行为，并允许运行时控制/监视此行为。 用户模式驱动程序将运转后台线程，为线程分配尽量低的优先级，并依赖于 NT 计划程序来确保这些线程不会干扰关键路径线程（一般会成功）。 请参阅 [PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062)。

* **驱动程序热更新**：需要更新 OS 组件时，尽量减少服务器停机时间。 请参阅 [DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate) 和 [DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate)。

### <a name="networking-1903"></a>网络

#### <a name="netadaptercx"></a>NetAdapterCx

在 NetAdapter WDF 类扩展 (NetAdapterCx) 中，网环缓冲区已由网环取代，后者提供新的接口用于通过网环迭代器发送和接收网络数据。 下面是新主题的列表：

* [网环和网环迭代器](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-rings-and-net-ring-iterators)
* [使用网环发送网络数据](https://docs.microsoft.com/windows-hardware/drivers/netcx/sending-network-data-with-net-rings)，其中提供了演示如何发送数据的新动画
* [使用网环接收网络数据](https://docs.microsoft.com/windows-hardware/drivers/netcx/receiving-network-data-with-net-rings)，其中提供了演示如何接收数据的新动画
* [使用网环取消网络数据](https://docs.microsoft.com/windows-hardware/drivers/netcx/canceling-network-data-with-net-rings)

支持此功能的新标头包括：

* [Ring.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/index)
* [Ringcollection.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ringcollection/index)
* [Netringiterator.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/index)

下面是 NetAdapterCx 内容更新的列表：

* 已删除默认的适配器对象，改用单个适配器对象类型。 已相应地更新了以下主题：

  * [NetAdapterCx 对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [设备和适配器初始化](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)

* 硬件卸载和数据包扩展 DDI 已重新组织为新标头：

  * [Checksum.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksum/index)
  * [Checksumtypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksumtypes/index)
  * [Extension.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extension/index)
  * [Lso.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lso/index)
  * [Lsotypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lsotypes/index)
  * [Rsc.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsc/index)
  * [Rsctypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsctypes/index)

* 基本网络数据结构、数据包和段已更新，并已放入新标头：

  * [Packet.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/index)
  * [Fragment.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fragment/index)

* 大幅修改了[传输和接收队列](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)主题，以包含回调示例和数据包队列的主要操作。

#### <a name="mobile-operator-scenarios"></a>移动运营商方案

编写了新的移动套餐内容，以方便移动运营商通过移动套餐应用直接在 Windows 10 设备上向客户销售套餐：

* [移动套餐](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/mobile-plans)

### <a name="mobilebroadband-1903"></a>移动宽带

以下功能已添加到 Windows 10 版本 1903 中的移动宽带：

* 新的 [SIM 卡 (UICC) 文件/应用程序系统访问](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-application-and-file-system-access)功能
* 新的[手机网络时间信息 (NITZ)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-nitz-support) 功能。
* 新的[使用 DSS 进行调制解调器日志记录](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-logging-with-dss)功能。
* 新的 [5G 数据类支持](https://docs.microsoft.com/windows-hardware/drivers/network/mb-5g-data-class-support)功能。

### <a name="print-1903"></a>打印

在 Windows 10 版本 1903 中添加的新打印驱动程序文档和功能包括：

* 新的 USB 打印 IOCTL：

  * [IOCTL_USBPRINT_GET_INTERFACE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_interface_type)
  * [IOCTL_USBPRINT_GET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_protocol)
  * [IOCTL_USBPRINT_SET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_set_protocol)

* 新的 **fpRegeneratePrintDeviceCapabilities** [PRINTPROVIDER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_printprovidor) 结构成员和更新的文档。

### <a name="sensors-1903"></a>传感器

Windows 10 版本 1903 中传感器驱动程序开发的新功能包括用于测试和校准屏幕亮度的 [MALT（Microsoft 环境光照度工具）](https://docs.microsoft.com/windows-hardware/drivers/sensors/testing-malt-building-a-light-testing-tool)。

此外，还更新了环境色 OEM 白皮书。

### <a name="storage-1903"></a>存储

Windows 10 版本 1903 中添加了以下存储功能：

* 添加了新的 Storport API，用于在 ETW 事件中记录设备故障和硬件协议错误，以及查询平台 D3 所需的行为
* 添加了新的 API 用于设置存储设备或适配器的属性
* 对于文件系统，已添加新的 DDI 用于支持在创建完成时检索扩展属性 (EA) 信息，使微型筛选器能够改变 ECP 有效负载来更改更高级别的筛选器看到的结果

### <a name="windows-hardware-error-architecture-whea"></a>Windows 硬件错误体系结构 (WHEA)

Windows 10 版本 1903 包含 WHEA 的简化界面。  有关详细信息，请参阅以下页：

* [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
* [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
* [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
* [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
* [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
* [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
* [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

### <a name="wifi-1903"></a>Wi-Fi

新的 Wi-Fi 驱动程序开发文档和功能包括：

* 新的精准时序测量(FTM) 功能
* 新的 [WPA3-SAE 身份验证](https://docs.microsoft.com/windows-hardware/drivers/network/wpa3-sae-authentication)功能
* 新的多频段操作 (MBO) 支持，可提高企业方案的漫游性能
* 新的信标报告卸载支持
* 有关这些新功能的 OID 命令、NDIS 状态指示和 TLV，请参阅 [WDI 文档更改历史记录](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-doc-change-history)

已更新 Windows 10 版本 1903 的以下主题：

* [WDI_AUTH_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm) - 添加了对 WPA3-SAE 身份验证的支持
* [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame) 和 [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-response-action-frame) - 对传出的点对点 (P2P) 动作帧添加了更多验证

## <a name="whats-new-in-windows-10-version-1809"></a>Windows 10 版本 1809 中的新增功能

本部分介绍 Windows 10 版本 1809（Windows 10 2018 年 10 月更新）中驱动程序开发的新增功能和更新。

[返回页首](#top)

### <a name="audio-1809"></a>音频

现已发布有关新的 [sidebandaudio](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sidebandaudio/) 和 [usbsidebandaudio](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbsidebandaudio/) 标头的文档。

### <a name="bluetooth-1809"></a>蓝牙

* HCI_VS_MSFT_Read_Supported_Features 已更新，包含用于安全简单配对过程的新标志。 请参阅 [Microsoft 定义的蓝牙 HCI 命令和事件](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/microsoft-defined-bluetooth-hci-commands-and-events#hcivsmsftreadsupportedfeatures)。

* 以下网页提供了 Windows 10 版本 1809 的新 QDID：[108589](https://launchstudio.bluetooth.com/ListingDetails/55701)。 有关所有版本的 QD ID 完整列表，请参阅[蓝牙](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)。

### <a name="display-1809"></a>显示

Windows 10 版本 1809 中的“显示”驱动程序开发的更新包括：

* **光线跟踪**：为了支持硬件加速的光线跟踪，我们在开发 Direct3D API 的同时开发了新的 Direct3D DDI。 示例 DDI 包括：[PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054)、[PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)。 有关光线跟踪的详细信息，请参阅[宣布推出 Microsoft DirectX 光线跟踪](https://blogs.msdn.microsoft.com/directx/2018/03/19/announcing-microsoft-directx-raytracing/)。

* **通用驱动程序要求**：WDDM 2.5 驱动程序需要确保其 DirectX11 UMD、DirectX12 UMD、KMD 以及这些组件加载的其他任何 DLL 遵守通用 API。

* **仅限 SRV 的平铺资源层 3**：在 Windows 10 版本 1809 中，GPU 能够更以更低的正交性支持平铺资源层 3 功能。 Direct3D12 现在支持稀疏体积纹理，而无需进行无序访问和渲染器目标操作。 仅限 SRV 的平铺资源层 3 是适合在第 2 层和第 3 层之间部署的概念层。 与当前的正交平铺资源层 3 一样，硬件支持是可选的。 但是，仅限 SRV 的平铺资源层 3 支持是一个超集层，需要平铺资源层 2 的支持。

   已播发正交平铺资源层 3 支持的驱动程序只需更新其驱动程序即可支持最新的“选项上限”DDI 结构版本。 对于已能支持正交平铺资源层 3 的任何硬件，运行时会将仅限 SRV 的平铺资源层 3 支持播发到应用程序。

* **渲染通道**：已添加渲染通道功能来实现以下目的：

  * 在现有的驱动程序上运行新的 API。
  * 使用户模式驱动程序能够选择最佳的渲染路径，且不会严重降低 CPU 的性能。

* **元命令**：元命令是代表 IHV 加速算法的 Direct3D12 对象。 它是对驱动程序实现的命令生成器的不透明引用。 元命令的更新包括描述符表绑定和纹理绑定。 请参阅 [D3D12DDI_META_COMMAND_PARAMETER_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ne-d3d12umddi-d3d12ddi_meta_command_parameter_type) 和 [D3D12DDIARG_META_COMMAND_PARAMETER_DESC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_meta_command_parameter_desc)。

  启用计算算法以使用纹理资源（重排内存）
  * 启用图形管道算法

* **HDR 亮度补偿**：引入了新的 SDR 亮度提升技术，以将 SDR 内容的参考白色部分提高到用户所需的值，这样就能够以 200-240 典型尼特值再现 SDR 内容，相当于用户预期的 SDR 显示效果。 SDR 亮度提升在两个方面会影响总体 Brightness3 行为：

  1. 只能在预先混合的前提下，针对 SDR 内容应用此提升。 HDR 内容不受影响。 同时，对于大多数笔记本电脑/brightness3 方案，用户预期所有内容（SDR 和 HDR）可调整。
  2. 当 OS 中的 Brightness3 堆栈确定所需的尼特值时，并不知道已经应用了 SDR 提升。

     驱动程序必须对来自 HDR Brightness3 DDI 的所需尼特值应用补偿。 由于图形驱动程序（和下游的 TCON 等）将会修改内容的像素值以获取所需的尼特值，因此，还应该对应用程序通过 [D3DDDI_HDR_METADATA_HDR10](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_hdr_metadata_hdr10) 提供的 HDR 内容元数据或者通过 [DxgkDdiSetTargetAdjustedColorimetry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry) 提供的 OS 默认值应用补偿。 由于图形驱动程序 (TCON) 负责修改像素数据，因此驱动程序需负责补偿 HDR 内容元数据。

* **HDR 像素格式支持**：此内核模式设备驱动程序接口 (DDI) 更改包含在 WDDM 2.5 中，公开了驱动程序/设备报告的新功能，提供有关驱动程序/设备支持的 HDR 功能的信息。

   目前，OS 根据从 [DdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo) 读取的 [DXGK_MONITORLINKINFO_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities) 结构的 *HighColorSpace* 位确定驱动程序/设备是否支持 HDR。 *HighColorSpace* 位提供以 HDR 模式运行的驱动程序/链接/监视功能的组合。

    驱动程序报告的 HDR 功能现在包括驱动程序/设备级功能，可让 OS 知道驱动程序/设备是支持真正的 HDR（即 FP16HDR），还是仅支持受限形式的 HDR（即 ARGB10HDR），相关定义如下：

  * FP16HDR：驱动程序/设备可将 FP16 像素格式图面与 scRGB/CCCS 色彩空间结合使用，并在运行扫描输出管道期间应用 PQ/2084 编码和 BT.2020 原色，以将输出信号转换为 HDR10。
  * ARGB10HDR：驱动程序/设备可以采用已经过 PQ/2084 编码的 ARGB10 像素格式图面，并扫描输出 HDR10 信号。 驱动程序/设备无法处理上面定义的 FP16HDR，也无法处理 scRGB FP16 的扩展数值范围。

    图形驱动程序只能报告 FP16HDR 或 ARGB10HDR 的支持，因为它们并不真正采用超集/子集配置；如果同时报告支持 FP16HDR 和 ARGB10HDR，则 OS 会使启动适配器失败。 请参阅 [DXGK_MONITORLINKINFO_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities) 和 [_DXGK_DISPLAY_DRIVERCAPS_EXTENSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_display_drivercaps_extension)。

* **SDR 白水平**：内核模式设备驱动程序接口的更改包括将新的参数添加到现有的 DDI，使图形驱动程序知道 OS 复合器对所有在 HDR 模式下显示的 SDR 内容应用的“SDR 白水平”值。 请参阅“_DXGK_COLORIMETRY”。

### <a name="kernel-1809"></a>Windows 内核

核心内核中添加了几个新的 API：

* [RtlQueryRegistryValueWithFallback 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlqueryregistryvaluewithfallback)：在缺少主句柄的情况下使用回退句柄查询注册表值项。
* [PsGetSiloContainerId 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetsilocontainerid)和 [PsGetThreadServerSilo 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetthreadserversilo)
* 已将新的信息类添加到 [_FILE_INFORMATION_CLASS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class)
  * FileLinkInformationExBypassAccessCheck
  * FileCaseSensitiveInformationForceAccessCheck
  * FileStorageReserveIdInformation
    * FileLinkInformationEx
* 已将扩展的 NtCreateSection 版本添加到 [NtCreateSectionEx 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatesectionex)，以指示这实际上是一个 AWE 节。
* 新的 Ex 宏授予对 Ntoskernel 导出的实际推送锁 API 的直接访问权限。
  * [ExAcquirePushLockExclusive 宏](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exacquirepushlockexclusive)
  * [ExAcquirePushLockShared 宏](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exacquirepushlockshared)
  * [ExInitializePushLock 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepushlock)
  * [ExReleasePushLockExclusive 宏](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleasepushlockexclusive)
  * [ExReleasePushLockShared 宏](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleasepushlockshared)
* [KzLowerIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kzlowerirql) 和 [KzRaiseIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kzraiseirql) 已移到面向 Windows 8 和更高版本的内核组件的受支持外部 forceinline，而不依赖于转发器来实例化内联函数的特殊用例。
* 平展 PCI 的门户桥 (FPB) 现在受支持。 有关详细信息，请参阅[官方规范](https://pcisig.com/sites/default/files/specification_documents/ECN_FPB_9_Feb_2017.pdf)。 在 [Ntddk.h](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/) 中声明了新的 API (_PCI_FPB_*)。

### <a name="networking-1809"></a>网络

#### <a name="netadaptercx"></a>NetAdapterCx

* 新的 [NetAdapterCx 客户端驱动程序的 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/netcx/inf-files-for-netadaptercx-client-drivers)主题。
* 传输和接收队列已合并成名为“数据包队列”的单个对象类型，以简化 API 图面。 已将标题为[轮询模型](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues#polling-model)的新部分添加到[传输和接收队列](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)主题。
* 已将[硬件卸载](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-hardware-offloads)添加到 NetAdapterCx，该功能还可以自动注册客户端驱动程序的关联数据包扩展。
* 网络接口现在与驱动程序的 WDF 设备对象分离。 为了支持此功能，现已删除 *EvtNetAdapterSetCapabilities* 回调函数。 NetAdapterCx 客户端驱动程序现在可以包含多个网络接口，其中包括一个默认接口。

   更新的有关支持网络接口/设备对象分离的主题包括：

  * [NetAdapterCx 对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [设备和适配器初始化](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)
  * [NetAdapterCx 客户端驱动程序的通电顺序](https://docs.microsoft.com/windows-hardware/drivers/netcx/power-up-sequence-for-a-netadaptercx-client-driver)
  * [NetAdapterCx 客户端驱动程序的断电顺序](https://docs.microsoft.com/windows-hardware/drivers/netcx/power-down-sequence-for-a-netadaptercx-client-driver)

* 支持 [NetAdapterCx 接收端缩放 (RSS)](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-receive-side-scaling-rss-) 的 DDI 已简化。
* 已删除数据包上下文标记帮助器宏。

#### <a name="ndis"></a>NDIS

[接收端缩放版本 2 (RSSv2)](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-) 已更新为版本 1.01。

### <a name="mobilebroadband-1809"></a>移动宽带

* 新的 [OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-mpdp) 和 DDI 可以支持 MBB 设备的多个数据包数据协议 (MPDP) 接口。
* 新的[基于设备的重置和恢复](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-based-reset-and-recovery)能够以更可靠的方式重置和恢复 MBB 设备与驱动程序。

#### <a name="mobile-broadband-wdf-class-extension-mbbcx"></a>移动宽带 WDF 类扩展 (MBBCx)

MBBCx 电源管理方法已简化。

尽管 Windows 10 版本 1803 中提供 MBBCx 的预览内容，但 Windows 10 版本 1809 的 WDK 版本中随附了 MBBCx。

#### <a name="mobile-operators"></a>移动运营商

现在，桌面版 COSA 支持 [AutoConnectOrder 设置](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings#apn-database-and-desktop-cosa-settings)。

### <a name="sensors-1809"></a>传感器

自动亮度调节功能支持：

已添加 PKEY_SensorData_IsValid 数据字段以支持传感器中的自动亮度调节。

有关详细信息，请参阅[光传感器数据字段](https://docs.microsoft.com/windows-hardware/drivers/sensors/light-sensor-data-fields)。

### <a name="usb-1809"></a>USB

**面向 USB 类型 C 驱动程序开发人员的新功能：**

如果硬件符合 UCSI 规范并且需要通过非 ACPI 传输进行通信，则你可以利用新的类扩展 &mdash; (UcmUcsiCx.sys)。 此扩展以传输无关的方式实现 UCSI 规范。 只需编写极少量的代码，驱动程序（即 UcmUcsiCx 的客户端）即可通过非 ACPI 传输来与 USB 类型 C 硬件通信。 本主题介绍 UCSI 类扩展提供的服务，以及客户端驱动程序的预期行为。

* [编写 UCSI 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-ucsi-driver)
* [UcmUcsiCx 类扩展参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)
* [UcmUcsiCx 客户端驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

**使用面向 USB 类型 C 驱动程序开发人员的新功能可以监视 USB 类型 C 连接器的活动和/或参与 USB 类型 C 连接器的策略决策。**

例如，根据热量状况控制设备的充电，使设备不会过热。

* [编写 USB 类型 C 策略管理器客户端驱动程序](https://microsoft.com/windows-hardware/drivers/usbcon/policy-manager-client)
* [Usbpmapi.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/) 中提供了新的 API

**适用于模拟 USB 设备 (UDE) - 1.1 和 USB 主控制器 (Ucx) 1.5 的新版类扩展：**

模拟设备现在可通过功能 (FLDR) 和平台 (PLDR) 重置来支持更好的重置和恢复。 客户端驱动程序现在可让系统知道设备需要重置以及重置的类型：功能或平台。

* [UdecxWdfDeviceNeedsReset 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

主控制器还可通过以下方式选择 FLDR 和 PLDR 重置：

* [EVT_UCX_USBDEVICE_DISABLE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)

### <a name="wifi-1809"></a>Wi-Fi

WLAN 设备驱动程序接口 (WDI) 规范已更新为版本 1.1.7。

* 添加了 WDI 驱动程序的最新 802.11ax PHY 类型的支持。
* 添加了未经请求的设备服务指示的支持。

## <a name="whats-new-in-windows-10-version-1803"></a>Windows 10 版本 1803 中的新增功能

本部分介绍 Windows 10 版本 1803（Windows 10 2018 年 4 月更新）中驱动程序开发的新增功能和更新。

[返回页首](#top)

### <a name="acpi-1803"></a>ACPI

Windows 10 版本 1803 包含 ACPI DDI 的更新，支持平台功能和物理设备定位。

### <a name="audio-1803"></a>音频

[语音激活](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)主题已更新，包括有关 APO 要求的附加信息。

### <a name="bluetooth-1803"></a>蓝牙

Windows 10 版本 1803 引入了迅速配对的支持。 用户不再需要在设置应用中导航并查找外设即可配对。 Windows 可以自动为用户完成配对。当附近出现新的外设并且该设备准备就绪时，Windows 会弹出一条通知。 确保外设进行迅速配对需要满足两套要求。 一套要求与外设的行为相关，另一套要求与 Microsoft 定义的供应商播发部分中的结构和值相关。 有关详细信息，请参阅：

* [蓝牙迅速配对](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth-swift-pair)
* [蓝牙功能和建议](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)

Windows 10 版本 1803 支持蓝牙版本 5.0。 有关配置文件支持的信息，请参阅 [Windows 10 中的蓝牙版本和配置文件支持](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/general-bluetooth-support-in-windows)。

### <a name="camera-1803"></a>相机

对相机驱动程序开发的更新包括：

* [适用于 UVC 设备的 DShow (DirectShow) 桥实施指南](https://docs.microsoft.com/windows-hardware/drivers/stream/dshow-bridge-implementation-guidance-for-usb-video-class-devices) - 有关配置符合 USB 视频类 (UVC) 规范的相机和设备的 DShow 桥的实施指南。 平台使用 USB 总线标准中的 Microsoft OS 描述符来配置 DShow 桥。 扩展属性 OS 描述符是 USB 标准描述符的扩展，USB 设备使用它来返回尚未通过标准规范启用的 Windows 特定设备属性。
* [全景相机视频捕获](https://docs.microsoft.com/windows-hardware/drivers/stream/360-camera-video-capture) - 使用现有的 MediaCapture API 提供全景相机预览、捕获和记录支持。 平台可以使用此功能来公开球形帧源（例如 equirectangular 帧），使应用能够检测和处理全景视频相机流，以及提供全景拍摄体验。

### <a name="display-1803"></a>显示

下面是对 Windows 10 版本 1803 中的“显示”驱动程序开发的更新：

* **间接显示 UMDF 类扩展** - 间接显示驱动程序可将 SRM 传递给渲染 GPU，并提供一种机制用于查询所用的 SRM 版本。

* **基于 IOMMU 硬件的 GPU 隔离支持** - 通过限制 GPU 访问系统内存来提高安全性。

* **GPU 半虚拟化支持** - 可让显示驱动程序在 Hyper-V 虚拟化环境中提供渲染功能。

* **亮度** - 提供新的亮度接口来支持多个显示器，这些显示器可设置为基于校准尼特值的亮度水平。

* **D3D11 位流加密** - 在 D3D11 中提供更多的 GUID 和参数来支持公开包含 8 或 16 字节初始化矢量的 CENC、CENS、CBC1 和 CBCS。

* **D3D11 和 D3D12 视频解码直方图** - 借助照度直方图，媒体团队可以利用直方图的固定功能硬件来改善 HDR/EDR 方案的音调映射质量。 当这些方案已经饱和使用了 GPU 或者想要启用并行处理时，固定功能硬件非常有用。 此功能是可选的。仅当固定功能硬件可用时，才应该实现此功能。 不应配合 3D 或计算方案实现此功能。

* **D3D12 视频解码**现在支持解码层 II，指示驱动程序支持纹理阵列，可在分辨率发生更改时，让应用程序分摊分配成本并减少峰值内存使用量。 

* **平铺资源层和 LDA 原子性** - 提供新的跨节点共享层，以添加对跨链接适配器 (LDA) 节点工作的原子着色器指令的支持。 这提高了 ISV 实现多种 GPU 渲染技术（例如分割帧渲染 (SFR)）的能力，并且与 D3D11 相比，将功能提高到了新的层次。

* **GPU 递色支持** - 驱动程序可以报告给定计时模式下针对网络信号执行递色的能力。 这样，当所需的位深度效率高于监视链路实际所能提供的效率时（例如需要 HDR10 而不是 HDMI 2.0），OS 可以显式请求递色。

* **后处理颜色增强覆盖** - 可让 OS 请求驱动程序暂时禁用任何增强或更改显示颜色的后处理功能。 这可以支持如下所述的方案：特定的应用程序能够以比色方式在显示器上实施准确的色彩行为，并安全地与 OEM 或 IHV 专属显示颜色增强功能共存。

* **Direct3D12 和视频** - 新的 API 和 DDI 提供对以下功能的访问：
  * 硬件加速的视频解码
  * 内容保护
  * 视频处理

* **DisplayID** - 一个新的 DDI，旨在通过受图形适配器控制的，并且应该支持 DisplayID v1.3 和 DisplayID v2.0 的显示器查询 VESA 的 DisplayID 描述符。 DDI 是现有 DxgkDdiQueryAdapterInfo DDI 的扩展，应受 DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM2_3 的所有驱动程序的支持，包括仅限内核模式显示的驱动程序和间接显示驱动程序。

* **GPU 性能数据** - DdiQueryAdapterInfo 的扩展将公开温度、风扇速度、引擎和内存时钟速度、内存带宽、功耗和电压等信息

* 杂项 - 新的 SupportContextlessPresent 驱动程序上限可帮助 IHV 载入新驱动程序。

* 改进了 OS 中的外部/可移动 GPU 支持。 作为改进支持的第一步，Dxgkrnl 需要确定 GPU 是否“可分离”，即可热插拔。 对于 RS4，我们希望利用此方面的驱动程序信息，而不是生成自己的基础结构。 为此，我们将在 DXGK_ DRIVERCAPS 结构中添加“Detachable”位。 如果适配器可热插拔，则在适配器初始化期间，驱动程序会设置此位。

* **显示诊断** - 内核模式设备驱动程序接口 (DDI) 已发生更改，允许显示控制器的驱动程序向 OS 报告诊断事件。  这就提供了一个通道来让驱动程序记录事件，否则 OS 看不到这些事件，因为事件不是 OS 请求的响应，也不是 OS 需要应对的对象。

* **共享图形电源组件** - 使非图形驱动程序能够参与图形设备的电源管理。  非图形驱动程序将配合图形驱动程序，使用某个驱动程序接口来管理其中一个或多个共享的电源组件。

* **共享纹理改进** - 包括增加了可在进程和 D3D 设备之间共享的纹理类型。 此设计使得帧服务器 OS 组件能够以极少量的内存复制来支持单色。

### <a name="security-1803"></a>驱动程序安全性

对 [Windows 驱动程序安全指南](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/)和[驱动程序安全清单](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/driver-security-checklist)做了更新，为驱动程序开发人员提供驱动程序安全清单。

### <a name="kernel-1803"></a>Windows 内核

本部分介绍 Windows 10 版本 1803 中的 Windows 内核驱动程序开发的新增功能和已更新的功能。

已将一组新 API 添加到工具包，使第三方能够创建其自己的 KDNET 扩展模块或 KdSerial 传输层。 有关示例代码，请参阅 Debuggers 文件夹中的“内核传输示例”(ddk\samples\kdserial and ddk\samples\kdnet)。

添加了相应的支持，为驱动程序提供一个可以存储文件状态的批准位置（操作系统知道该位置）。  使用此方法时，系统可将该位置中的文件与某个设备或驱动程序相关联。

有不同的位置用于存储特定于驱动程序内部组件或特定于设备的文件状态。 对于包含文件状态的驱动程序，可以确定写入到磁盘的状态是：

* 驱动程序状态 ([IoGetDriverDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdriverdirectory))：可能正在控制多个设备的驱动程序的全局状态，还是

* 设备状态 ([IoGetDeviceDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdevicedirectory))：特定于驱动程序控制的单个设备，其他设备可能对类似的状态使用不同的值。

现在，当功能驱动程序 (FDO) 的相应 PCIe 设备处于 D3Cold 状态时，可与其他电源协商。 这包括：

* 辅助电源要求 [D3COLD_REQUEST_AUX_POWER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-d3cold_request_aux_power)。
* 核心电源导轨 [D3COLD_REQUEST_CORE_POWER_RAIL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-d3cold_request_core_power_rail)。
* 在从 PCI Express 下游端口收到消息，到相应终结点或 PCI Express 下游端口在系统处于 ACPI 工作状态时转换为 D3cold 期间平台将 PERST# 断言到插槽的固定延迟时间要求。 请参阅 [D3COLD_REQUEST_PERST_DELAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-d3cold_request_perst_delay)。

NT 服务以及内核模式和用户模式驱动程序可以使用 [RtlRaiseCustomSystemEventTrigger](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlraisecustomsystemeventtrigger) 函数针对设备引发自定义触发器。 驱动程序开发人员拥有的自定义触发器通知系统事件代理使用自定义触发器标识符标识的触发器启动关联的后台任务。

现在，可以在激发通知时注册活动会话更改通知并获取回调。 作为此通知的一部分，某些数据还会与调用方共享。 这些关联的数据通过 [PO_SPR_ACTIVE_SESSION_DATA 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntpoapi/ns-ntpoapi-_po_spr_active_session_data)传送。

### <a name="networking-1803"></a>网络

本部分概述 Windows 10 版本 1803 中 Windows 网络驱动程序开发的新增功能和改进。

#### <a name="ndis-and-netadaptercx"></a>NDIS 和 NetAdapterCx

NDIS 的更新包括：

* [接收端缩放 V2](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-in-ndis-6-80) 已更新，包括有关操纵参数的更多详细信息
* [同步 OID 接口](https://docs.microsoft.com/windows-hardware/drivers/network/synchronous-oid-request-interface-in-ndis-6-80)现在支持 NDIS 轻型筛选器驱动程序

下面是网络适配器 WDF 类扩展 (NetAdapterCx) 的新主题：

* [NetAdapterCx 1.2 简介](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-netadaptercx-1-2)
* [数据包描述符和扩展](https://docs.microsoft.com/windows-hardware/drivers/netcx/packet-descriptors-and-extensions)
* [网络数据缓冲区管理](https://docs.microsoft.com/windows-hardware/drivers/netcx/network-data-buffer-management)
* [NetAdapterCx 接收端缩放 (RSS)](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-receive-side-scaling-rss-)

此外，为仅限预览的功能 - 移动宽带类扩展 (MBBCx) 提供了新的主题。该功能使用 NetAdapterCx 模型建立移动宽带连接。

* [移动宽带类扩展 (MBBCx)](https://docs.microsoft.com/windows-hardware/drivers/netcx/mobile-broadband-mbb-wdf-class-extension-mbbcx-)
  * [编写 MBBCx 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/netcx/writing-an-mbbcx-client-driver)
  * [MBBCx API 参考](https://docs.microsoft.com/windows-hardware/drivers/netcx/mbbcx-api-reference)

### <a name="mobilebroadband-1803"></a>移动宽带

在移动宽带中，提供了详细介绍 [MB 低级别 UICC 访问](https://docs.microsoft.com/windows-hardware/drivers/network/mb-low-level-uicc-access)的新主题。

#### <a name="mobile-operators"></a>移动运营商

[桌面版 COSA](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings#desktop-cosa-only-settings) 现在包括新的热点和 AppID 设置。 强烈建议移动运营商从使用 [Sysdev 元数据包](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata)的宽带应用体验过渡到 [MO UWP 应用](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/uwp-mobile-broadband-apps)和 [COSA 数据库](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings)。

### <a name="pci-1803"></a>PCIe

添加了新的 ACPI _DSD 方法用于支持以下新式待机和 PCI 热插拔方案：

* PCIe 根端口上的定向最深运行时空闲电源状态 (DDRIPS) 支持
* 在 D3 中识别支持热插拔的 PCIe 根端口
* 识别外部公开的 PCIe 根端口

有关信息，请参阅 [ACPI 接口：PCIe 根端口的设备特定数据 (_DSD)](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports)。

### <a name="sensors-1803"></a>传感器

添加了 [SENSOR_CONNECTION_TYPES 枚举](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-sensor_connection_types)用于澄清连接类型属性。

### <a name="usb-1803"></a>USB

添加了新的 API 用于模拟共享连接器的分离。 如果 USB 设备已附加到主机，或者在删除堆栈时包含共享连接器，则你可以模拟分离事件。 此时已禁用所有附加/分离通知机制。 有关详细信息，请参阅 [UfxDeviceNotifyFinalExit 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyfinalexit)。

### <a name="wifi-1803"></a>Wi-Fi

Wi-Fi 驱动程序开发的更新包括添加了新的[用于 NIC 自动电源保护程序 (NAPS) 高级电源管理的 TLV 功能](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-os-power-management-features)，以及对平台级设备恢复服务 (PLDR) 的更新。

## <a name="whats-new-in-windows-10-version-1709"></a>Windows 10 版本 1709 中的新增功能

本部分介绍 Windows 10 版本 1709 中驱动程序开发的新增功能和更新。

[返回页首](#top)

### <a name="audio-1709"></a>音频

下面是 Windows 10 版本 1709 中 Windows 音频驱动程序开发的更新列表：

* 新的[配置和查询音频设备模块](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)
* 对[语音激活](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)做了大量更新
  * 有关仅限链接和关键字激活的更多详细信息
  * 新的词汇表
  * 有关训练和识别的更多信息，例如引脚和音频格式信息
  * 更新的关键字系统概述
  * 有关语音唤醒的更新信息

### <a name="acpi-1709"></a>ACPI

下面是用于支持输入/输出缓冲区的新高级配置和电源接口 (ACPI) DDI 列表。

* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)
* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)
* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2)
* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2_ex)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2_ex)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2_ex)
* [ACPI_EVAL_INPUT_BUFFER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)
* [ACPI_EVAL_INPUT_BUFFER_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)
* [ACPI_EVAL_INPUT_BUFFER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2)
* [ACPI_EVAL_INPUT_BUFFER_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2_ex)
* [ACPI_EVAL_OUTPUT_BUFFER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)
* [ACPI_EVAL_OUTPUT_BUFFER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v2)
* [ACPI_METHOD_ARGUMENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)
* [ACPI_METHOD_ARGUMENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v2)
* [GIC_ITS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpitabl/ns-acpitabl-_gic_its)

### <a name="biometric-1709"></a>生物识别

Windows 生物识别驱动程序有新的签名要求。 有关详细信息，请参阅[为 WBDI 驱动程序签名](https://docs.microsoft.com/windows-hardware/drivers/biometric/signing-wbdi-drivers)。

### <a name="display-1709"></a>显示

下面是 Windows 10 版本 1709 中 Windows 显示驱动程序开发的新增功能列表。

* 显示色彩空间转换 DDI 针对合成后显示管道中应用的色彩空间转换提供更高的控制度。
* D3D12 复制队列时间戳查询功能可让应用程序针对 COPY 命令列表/队列发出时间戳查询。 这些时间戳的指定运行方式与其他引擎中的时间戳相同。
* 通过以下方式增强了视频与 Direct3D12 运行时的集成：
    1. 硬件加速的视频解码
    2. 内容保护
    3. 视频处理

### <a name="hardware-notifications-1709"></a>硬件通知

Windows 10 版本 1709 为 LED 和振动机制等通知组件提供不区分硬件的支持。 有关详细信息，请参阅：

* [硬件通知支持](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/hardware-notifications-support)
* [硬件通知参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_gpiobtn/)

### <a name="kernel-1709"></a>Windows 内核

在 Windows 10 版本 1709 中，为驱动程序的 Windows 内核添加了多个新例程。

* ExGetFirmwareType 和 ExIsSoftBoot &ndash; 执行库支持例程。
* [PsSetLoadImageNotifyRoutineEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetloadimagenotifyroutineex) &ndash; 针对所有可执行映像的扩展映像通知例程，包括其体系结构与操作系统本机体系结构不同的映像。
* [MmMapMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapmdl) &ndash; [内存管理器](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager)例程，用于将内存描述符列表 (MDL) 描述的物理页面映射到系统虚拟地址空间。
* [PoFxSetTargetDripsDevicePowerState ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsettargetdripsdevicepowerstate) &ndash; 一个 PoFx 例程，用于向电源管理器告知 DRIPS 的设备目标电源状态。
* 下面是 [ZwSetInformationThread](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwsetinformationthread) 例程的与处理策略相关的新选项列表：

  * [PROCESS_MITIGATION_CHILD_PROCESS_POLICY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_process_mitigation_child_process_policy)
  * [PROCESS_MITIGATION_PAYLOAD_RESTRICTION_POLICY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_process_mitigation_payload_restriction_policy)
  * PROCESS_READWRITEVM_LOGGING_INFORMATION

* [PsGetServerSiloActiveConsoleId](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetserversiloactiveconsoleid) 和 [PsGetParentSilo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetparentsilo) &ndash; 新的接收器 API，用于获取有关计算机上创建和销毁的服务器接收器的信息。
* 下面是新的 RTL 函数列表，通过这些函数可以使用关联矢量来引用事件和生成的日志，以进行诊断。
  * [CORRELATION_VECTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-correlation_vector)
  * [RtlExtendCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlextendcorrelationvector)
  * [RtlIncrementCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlincrementcorrelationvector)
  * [RtlInitializeCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlinitializecorrelationvector)
  * [RtlValidateCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlvalidatecorrelationvector)

### <a name="mobilebroadband-1709"></a>移动宽带

下面是适用于 Windows 10 版本 1709 中驱动程序开发的 Windows 移动宽带和移动运营商方案的新增功能列表：

* [UICC 重置](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-reset-operations)和[调制解调器重置](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-reset-operations)
* [协议配置操作 (PCO)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-protocol-configuration-operations--pco-)
* [基站信息查询](https://docs.microsoft.com/windows-hardware/drivers/network/mb-base-stations-information-query-support)
* [eSIM 卡和 MBIM ReadyState 指南](https://docs.microsoft.com/windows-hardware/drivers/network/mb-esim-mbim-ready-state-guidance)

在 Windows 10 版本 1709 中，[桌面版 COSA 文档](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/planning-your-desktop-cosa-apn-database-submission)已更新，包括新的品牌相关字段。
有关对移动运营商方案所做的其他更改，请参阅[已弃用的功能](#deprecated-features)列表。

### <a name="networking-1709"></a>网络

本部分概述 Windows 10 版本 1709 中 Windows 网络驱动程序开发的新增功能和改进。

下面是 NDIS 的新增功能和已更新功能列表：

* NetAdapterCx 1.1 简介，其中包括新的 NewAdapterCx 功能：
  * 更多的数据包上下文选项
  * 更精细的链接状态控制
  * 改进了接收缓冲区管理和性能
  * 一般性能改进
* NDIS 6.80 中新的[同步 OID 请求接口](https://docs.microsoft.com/windows-hardware/drivers/network/synchronous-oid-request-interface-in-ndis-6-80)
* NDIS 6.80 中新的[接收端缩放版本 2 (RSSv2)](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-in-ndis-6-80)
* [NDIS 6.80 简介](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-ndis-6-80)
* [将 NDIS 6.x 驱动程序移植到 NDIS 6.80](https://docs.microsoft.com/windows-hardware/drivers/network/porting-ndis-6-x-drivers-to-ndis-6-80)

### <a name="pci-1709"></a>虚拟化 PCI

提供新的编程接口用于编写符合 PCI Express 单根 I/O 虚拟化 (SR-IOV) 规范的设备的物理功能驱动程序。 接口在 Pcivirt.h 中声明。 有关详细信息，请参阅 [PCI 虚拟化](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pcivirt/)。

### <a name="pwm-1709"></a>脉宽调制 (PWM) 控制器

在 Windows 10 版本 1709 中，若要提供对已映射到 SoC 地址空间的 SoC 和内存中的脉宽调制 (PWM) 控制器的访问，需要编写一个内核模式驱动程序。 有关详细信息，请参阅 [SoC 中 PWM 模块的 PWM 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/spb/pulse-width-controller%20driver?branch=spb)。

若要分析和验证引脚路径和提取引脚编号，内核模型驱动程序应使用 [PwmParsePinPath](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pwmutil/nf-pwmutil-pwmparsepinpath)。

应用可以通过发送 [PWM IOCTL](https://docs.microsoft.com/windows-hardware/drivers/spb/pulse-width-controller%20driver#pwm-ioctl-requests) 请求，将请求发送到控制器驱动程序。

### <a name="storage-1709"></a>存储和文件系统

Windows 10 版本 1709 的文件系统和存储中添加了 ufs.h 标头，以提供对通用闪存存储的额外支持。

Posix 更新包括新的 **delete** 和 **rename** 函数。

下面是 Windows 10 版本 1709 中已更新的标头列表：

* ata.h
* fltKernel.h
* minitape.h
* ntddscsi.h
* ntddstor.h
* ntddvol.h
* ntifs.h
* scsi.h
* storport.h

### <a name="usb-1709"></a>USB

本部分介绍 Windows 10 版本 1709 中 USB 的新增功能。

#### <a name="media-agnostic-usb-ma-usb-protocol"></a>不区分媒体的 USB (MA-USB) 协议

USB 驱动程序堆栈可以使用不区分媒体的 USB (MA-USB) 协议，通过非 USB 物理媒体（例如 Wi-Fi）发送 USB 数据包。 为了实现此功能，我们已发布新的编程接口。 新的 DDI 可让驱动程序确定与 [_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays) 关联的延迟。 可以通过生成新的 URB 请求来检索该信息。
有关此新增功能的信息，请参阅以下主题：

* [不区分媒体的 (MA-USB) 协议的客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-client-drivers-for-ma-usb)
* [_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays)
* [USB 请求块 (URB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/communicating-with-a-usb-device)

若要支持 MA-USB，主控制器驱动程序必须通过实现特定的回调函数来提供传输特征。 下表显示了支持 MA-USB 的回调函数和结构。

| 回调函数 | 结构 |
| ----- | ----- |
| [EVT_UCX_USBDEVICE_GET_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_get_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |
| [EVT_UCX_USBDEVICE_RESUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_resume) | [UCX_CONTROLLER_ENDPOINT_CHARACTERISTIC_PRIORITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_priority) |
| [EVT_UCX_USBDEVICE_SUSPEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_suspend) | [UCX_ENDPOINT_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_characteristic) |
| [EVT_UCX_ENDPOINT_GET_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_get_isoch_transfer_path_delays) | [UCX_ENDPOINT_CHARACTERISTIC_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_type) |
| [EVT_UCX_ENDPOINT_SET_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_set_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |

#### <a name="synchronized-system-qpc-with-usb-frame-and-microframes"></a>系统 QPC 与 USB 帧和微帧同步

有新的编程接口可用于检索与帧和微帧同步的系统查询性能计数器 (QPC) 值。

仅当调用方在主控制器中启用了该功能时，才可以检索此信息。 若要启用此功能，主控制器驱动程序必须实现以下回调函数。

* [EVT_UCX_CONTROLLER_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_frame_number_and_qpc_for_time_sync)
* [EVT_UCX_CONTROLLER_START_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_start_tracking_for_time_sync)
* [EVT_UCX_CONTROLLER_STOP_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_stop_tracking_for_time_sync)

应用程序可以使用以下 API 来启用/禁用该功能以及检索信息：

* [WinUsb_GetCurrentFrameNumberAndQpc](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumberandqpc)
* [WinUsb_StartTrackingForTimeSync](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_starttrackingfortimesync)
* [WinUsb_StopTrackingForTimeSync](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_stoptrackingfortimesync)

其他驱动程序可以发送以下 IOCTL 请求来启用/禁用该功能以及检索信息：

* [IOCTL_USB_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_frame_number_and_qpc_for_time_sync)
* [IOCTL_USB_START_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_start_tracking_for_time_sync)
* [IOCTL_USB_STOP_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_stop_tracking_for_time_sync)

下面是与 USB 帧和微帧同步的系统 OPC 的支持结构：

* [USB_START_TRACKING_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_start_tracking_for_time_sync_information)
* [USB_STOP_TRACKING_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_stop_tracking_for_time_sync_information)
* [USB_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_frame_number_and_qpc_for_time_sync_information)

#### <a name="ioctlucmtcpciportcontrollerdisplayportdisplayoutstatuschanged"></a>IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED

[IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtcpciportcontrollerrequests/ni-ucmtcpciportcontrollerrequests-ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed) 请求是 USB 类型 C 端口控制器接口框架扩展中的新请求。 此请求向客户端驱动程序告知 DisplayPort 连接的显示输出状态已更改。

下面是支持 IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED 请求的结构：

* [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED_IN_PARAMS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtcpciportcontrollerrequests/ns-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status_changed_in_params)
* [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtcpciportcontrollerrequests/ne-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status)

## <a name="whats-new-in-windows-10-version-1703"></a>Windows 10 版本 1703 中的新增功能

本部分介绍 Windows 10 版本 1703 中驱动程序开发的新增功能和已改进的功能。

[返回页首](#top)

### <a name="audio-1703"></a>音频

下面是 Windows 10 版本 1703 中音频驱动程序开发的新主题列表：

* [实现音频模块通信](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication) - 介绍从通用 Windows 平台 (UWP) 应用到内核模式音频设备驱动程序的通信支持。
* 有关支持 APO 模块通信发现的新 DDI 和属性参考主题：
  * [KSPROPSETID_AudioModule](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audiomodule) - 用于定义特定于音频模块的三个属性的新 KS 属性集。
  * [KSPROPERTY_AUDIOMODULE_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-command) 属性 - 可让音频模块客户端发送自定义命令以查询和设置音频模块的参数。
  * [IPortClsNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsnotifications) - 新的端口类通知，用于提供微型端口的通知帮助器来支持音频模块通信。

### <a name="bluetooth-1703"></a>蓝牙

下面是 Windows 10 版本 1703 中蓝牙的更新列表：

* Windows 10 桌面版中包含宽带语音的免持配置文件 (HFP) 1.6 规范。
* Windows 10 桌面版中的[呼叫控制 API](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Calls) 支持。
* GATT 服务器、蓝牙 LE 外设支持和蓝牙 LE 的非配对支持。 有关更多详细信息，请参阅[开发人员文章](https://aka.ms/bluetoothgatt)。

有关蓝牙新增功能的详细信息，请参阅[蓝牙](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)和[蓝牙 LE 预配对](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth-prepairing)。

### <a name="camera-1703"></a>相机

下面是 Windows 10 版本 1703 中相机驱动程序开发的更新列表：

* [USB 视频类 (UVC) 驱动程序实施指南](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-driver-implementation-checklist)
* [USB 视频类 1.5 规范的 Microsoft 扩展](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)
* [设备转换管理器 (DTM) 事件](https://docs.microsoft.com/windows-hardware/drivers/stream/device-mft-events)
* [IMFDeviceTransform 接口](https://docs.microsoft.com/windows/desktop/api/mftransform/nn-mftransform-imfdevicetransform)
* KSCategory_Xxx 设备接口类
  * [KSCATEGORY_SENSOR_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-sensor-camera)
  * [KSCATEGORY_VIDEO_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video-camera)

### <a name="kernel-1703"></a>Windows 内核

[Windows 内核模式进程和线程管理器](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-process-and-thread-manager) - 从 Windows 10 版本 1703 开始，适用于 Linux 的 Windows 子系统 (WSL) 可让用户在 Windows 上连同其他 Windows 应用程序一起运行本机 Linux ELF64 二进制文件。 有关 WSL 体系结构以及运行二进制文件所需的用户模式和内核模式组件的详细信息，请参阅[适用于 Linux 的 Windows 子系统](https://blogs.msdn.microsoft.com/wsl/)博客中的文章。

### <a name="mobilebroadband-1703"></a>移动宽带

[**移动宽带 (MB)** ](https://docs.microsoft.com/windows-hardware/drivers/network/mobile-broadband--mb--design-guide) 的更新包括改进了 [LTE 附加功能](https://docs.microsoft.com/windows-hardware/drivers/network/mb-lte-attach-operations)、支持[多 SIM 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-multi-sim-operations)、支持调制解调器中的[预配上下文](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provisioned-context-operations)、支持[特定吸收率平台](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)，以及支持[网络黑名单](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)。

[**移动运营商方案 (MO)** ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/apn-database-overview) 的更新包括名为 [COSA FAQ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/cosa-overview) 的新数据库格式，可让 MO 预配 Windows 桌面 MB 设备。 有关其他更新，请参阅以下主题：

* [规划 COSA/APN 数据库提交](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/planning-your-desktop-cosa-apn-database-submission)
* [提交 COSA/APN 数据库更新](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/submitting-the-desktop-cosa-apn-database-update)
* [测试 COSA/APN 数据库提交](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/testing-your-desktop-cosa-apn-database-submission)

### <a name="networking-1703"></a>网络

Windows 10 版本 1703 中的网络驱动程序开发更新包括名为“流套接字”的新套接字类型，该类型支持 Windows 上的 Linux 网络应用程序。 有关详细信息，请参阅 [**Winsock 内核**](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)。 新的函数和结构包括 [WskConnectEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_connect_ex)、[WskListen](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_listen)、[WSK_CLIENT_STREAM_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_client_stream_dispatch) 和 [WSK_PROVIDER_STREAM_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_stream_dispatch)

### <a name="pos-1703"></a>POS

下面是 Windows 10 版本 1703 中 POS 的新主题列表：

* [蓝牙条形码扫描仪 UUID](https://docs.microsoft.com/windows-hardware/drivers/pos/barcode-scanner-bluetooth-service-uuids)
* [BarcodeSymbologyDecodeLenthType 枚举](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodesymbologydecodelengthtype)
* [BarcodeSymbologyAttributesData 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ns-pointofservicecommontypes-_barcodesymbologyattributesdata)

[BarcodeSymbology 枚举](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodesymbology)有新的 Gs1DWCode 符号。

### <a name="usb-1703"></a>USB

Windows 10 版本 1703 提供新的类扩展 (UcmTcpciCx.sys) 用于支持通用串行总线类型 C 端口控制器接口规范。 USB 类型 C 连接器驱动程序不需要保留任何内部的 PD/类型 C 状态。 管理 USB C 型连接器和 USB 电源输送 (PD) 状态机时存在的复杂性由系统处理。 你只需编写一个客户端驱动程序，以便通过该类扩展将硬件事件传送给系统即可。 有关详细信息，请参阅 [USB 类型 C 控制器接口驱动程序类扩展参考](https://msdn.microsoft.com/library/windows/hardware/mt805826)。

## <a name="whats-new-in-windows-10-version-1607"></a>Windows 10 版本 1607 中的新增功能

[返回页首](#top)

本部分介绍 Windows 10 版本 1607 中驱动程序开发的新增功能和改进。

### <a name="audio-1607"></a>音频

下面是 Windows 10 版本 1607 中音频驱动程序开发的新主题列表。

* [Windows 音频体系结构](https://docs.microsoft.com/windows-hardware/drivers/audio/windows-audio-architecture)
* 可以更好地支持 Cortana 体验的结构和属性：
  * [**KSPROPERTY\_AUDIO\_MIC\_SENSITIVITY**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mic-sensitivity)
  * [**KSPROPERTY\_AUDIO\_MIC\_SNR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mic-snr)
  * [**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)
* [PKEY\_AudioEndpoint\_Default\_VolumeInDb](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-audioendpoint-default-volumeindb) &ndash; 一个 INF 键，将相应的增益或衰减应用到音频信号时，该键可为用户提供更好的体验。

### <a name="camera-1607"></a>相机

Windows 10 版本 1607 中的相机驱动程序开发包括新的和更新的主题，以支持 Windows Hello 和人脸身份验证：

* [Windows Hello 相机驱动程序启动指南](https://docs.microsoft.com/windows-hardware/drivers/stream/windows-hello-camera-driver-bring-up-guide)
* [扩展的相机控制](https://docs.microsoft.com/windows-hardware/drivers/stream/standardized-extended-controls-)
* [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)

### <a name="location-1607"></a>定位

Windows 10 版本 1607 中的定位驱动程序开发包括以下新的 GNSS 痕迹导航 DDI：

* [**GNSS\_BREADCRUMB\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumb_list)
* [**GNSS\_BREADCRUMB\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumb_v1)
* [**GNSS\_BREADCRUMBING\_ALERT\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumbing_alert_data)
* [**GNSS\_BREADCRUMBING\_PARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumbing_param)
* [**IOCTL\_GNSS\_LISTEN\_BREADCRUMBING\_ALERT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_breadcrumbing_alert)
* [**IOCTL\_GNSS\_POP\_BREADCRUMBS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_pop_breadcrumbs)
* [**IOCTL\_GNSS\_START\_BREADCRUMBING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_start_breadcrumbing)
* [**IOCTL\_GNSS\_STOP\_BREADCRUMBING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_stop_breadcrumbing)

### <a name="print-1607"></a>打印

Windows 10 版本 1607 中的打印机驱动程序开发包括 [JSConstraintsDebug](https://docs.microsoft.com/windows-hardware/drivers/devtest/jsconstraintsdebug)，它是一个命令行工具，在开发 V4 打印机驱动程序时，可针对 JavaScript 约束提供调试支持。

### <a name="wlan-1607"></a>WLAN

在 Windows 10 版本 1607 中，为 WLAN 设备驱动程序接口 (WDI) 版本 1.0.21 提供了新的和更新的主题。 有关详细信息，请参阅 [WDI 文档更改历史记录](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-doc-change-history)。

## <a name="whats-new-in-windows-10-version-1507"></a>Windows 10 版本 1507 中的新增功能

[返回页首](#top)

本部分介绍 Windows 10 中驱动程序开发的新增功能和已更新的功能。

### <a name="bluetooth-1507"></a>蓝牙

在 Windows 10 中，添加了新的 [Microsoft 定义的蓝牙 HCI 扩展](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/microsoft-defined-bluetooth-hci-commands-and-events)。

### <a name="buses-and-ports"></a>总线和端口

Windows 的基于 OneCoreUAP 的版本包含适用于简单外设总线 (SPB)（例如 I2C 和 SPI）以及 GPIO 的驱动程序编程接口和现成驱动程序。 这些驱动程序可在 Windows 10 桌面版、Windows 10 移动版和其他 Windows 10 版本上运行。

### <a name="camera-1507"></a>相机

相机驱动程序 DDI 已融合到通用 Windows 驱动程序模型中，包括新的[相机 DDI](https://docs.microsoft.com/windows-hardware/drivers/stream/windows-10-technical-preview-camera-drivers-reference)。 其他功能包括：

* [数字视频防抖](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-videostabilization)
* [可变帧速率](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-vfr)
* [人脸检测](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-facedetection)
* [视频高动态范围 (HDR)](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-videohdr)
* [光学防抖](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-ois)
* [场景分析：照片 HDR、闪光、无闪光、超微光](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-advancedphoto)
* [捕获统计信息：元数据框架/属性、直方图](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-histogram)
* [平滑缩放](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)
* [硬件优化提示](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint-)
* [相机配置文件](https://docs.microsoft.com/windows-hardware/drivers/stream/camera-driver-functions)

### <a name="cellular"></a>手机网络

Windows 10 的[手机网络体系结构和实现](https://docs.microsoft.com/windows-hardware/drivers/network/cellular-architecture-and-driver-model)已更新。

### <a name="display-1507"></a>显示

Windows 8.1 和 Windows Phone 中的[显示驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_display/)已融合到 Windows 10 的统一模型。

实现了新的内存模型，可为每个 GPU 提供一个进程虚拟地址空间。 对于需要视频内存直接寻址的图形硬件，WDDMv2 仍然支持此寻址方式，但这种用例被视为已过时。 IHV 有望开发出支持虚拟寻址的新硬件。 为了支持这种新的内存模型，我们对 DDI 做了重大更改。

### <a name="human-interface-device"></a>人机接口设备 (HID)

新的虚拟 HID 框架 (VHF) 消除了编写内核模式传输微型驱动程序的需要。 该框架包括 Microsoft 提供的静态库 (Vhfkm.lib)，该库可公开驱动程序使用的编程元素。 此外，它还包括 Microsoft 提供的现成驱动程序 (Vhf.sys)，该驱动程序可以枚举一个或多个子设备，并继续生成虚拟的[人机接口设备](https://docs.microsoft.com/windows-hardware/drivers/hid/) (HID) 树。

* [使用虚拟 HID 框架 (VHF) 编写 HID 源驱动程序](https://docs.microsoft.com/windows-hardware/drivers/hid/virtual-hid-framework--vhf-)
* [虚拟 HID 框架](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vhf/)

### <a name="location-1507"></a>定位

全球导航卫星系统 (GNSS) 驱动程序 DDI 已融合到 [GNSS 通用 Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_gnss/) (UMDF 2.0)。

### <a name="near-field-communication"></a>近场通信 (NFC)

[NFC DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_nfpdrivers/) 包含新的融合驱动程序模型用于支持移动和桌面解决方案。

[NFC 类扩展](https://docs.microsoft.com/windows-hardware/drivers/nfc/nfc-class-extension-)：推出了新的 NFC 类扩展驱动程序。 该 NFC 类扩展驱动程序实现 Windows 定义的所有 DDI，以便与 NFC 控制器、安全元素和远程 RF 终结点交互。

### <a name="networking-1507"></a>网络

在现有的 NDIS 微型端口驱动程序模型中以扩展的形式推出了新的 [PacketDirect 提供程序接口 (PDPI)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-ndis-pdpi)。 PDPI 提供一个 I/O 模型，可让应用程序管理自身的缓冲区、轮询处理器，以及直接管理通过微型端口适配器发送和接收数据包的操作。 将这些功能相结合，应用程序可以完全控制其自身的上下文，从而大大提高每秒数据包 (pps) 的传输速率。

### <a name="print-1507"></a>打印

已使用 v4 打印驱动程序改进和更改对打印驱动程序做了更新，以支持通过移动设备进行无线打印；更新的功能还包括：

* [V4 驱动程序清单](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-manifest) &ndash; 提供有关对 v4 打印驱动程序清单所做的更改，以支持 PWG 光栅渲染筛选器的信息，包括更新的 DriverConfig 和 DriverRender 指令，以及更新的示例清单。
* [WS-Discovery 移动打印支持](https://docs.microsoft.com/windows-hardware/drivers/print/ws-discovery-mobile-printing-support) &ndash; 描述在 Windows 10 移动设备上通过 Windows 10 移动版兼容打印机进行移动打印所要满足的 WS-Discovery 要求。
* [**IXpsRasterizationFactory2 接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory2) &ndash; 支持使用 XPS 光栅化服务执行从 XPS 到 PWG 光栅的打印机内容转换。 PWG 光栅支持非矩形 DPI。
* [**打印管道属性包**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag) &ndash; 新的 PrintDeviceCapabilities 属性，可让 XPS 渲染筛选器从打印筛选管道属性包中检索新的 PrintDeviceCapabilities XML 文件。
* [GetWithArgument 请求和响应架构](https://docs.microsoft.com/windows-hardware/drivers/print/getwithargument-request-and-response-schemas) &ndash; 使用 GetWithArgument 请求和响应双向通信架构的正式定义与示例提供移动打印支持。
* [**IBidiSpl::SendRecv 方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl-sendrecv) &ndash; 使用 GetWithArgument 双向架构值添加移动打印支持。

### <a name="smart-card"></a>智能卡

在 Windows 10 中，新的类扩展模块 Wudfsmcclassext.dll 可以处理复杂的驱动程序操作。 特定于智能卡硬件的任务将由客户端驱动程序处理。 客户端驱动程序可以使用新的编程接口将有关智能卡的信息发送到该类扩展，使它可以处理请求。 这些驱动程序编程接口包含在 Windows 的基于 OneCoreUAP 的版本中。

* [智能卡客户端驱动程序事件回调函数](https://msdn.microsoft.com/library/windows/hardware/dn946583)
* [智能卡客户端驱动程序支持方法](https://msdn.microsoft.com/library/windows/hardware/dn946584)

### <a name="storage-1507"></a>存储

在 Windows 10 中，已添加新的特定于协议的接口，使应用能够使用其本机设备协议来与存储设备通信。 这些更新包括：

* 存储协议直通 &ndash; 更新的存储直通 IOCTL 接口支持较新的协议，包括非易失性快速存储器 (NVMe)。
* 扩展的存储查询接口 &ndash; 扩展的存储查询接口可让应用程序查询协议相关的信息。

### <a name="system-supplied-driver-interfaces"></a>系统提供的驱动程序接口

[GUID\_DEVICE\_RESET\_INTERFACE\_STANDARD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_reset_interface_standard) 接口定义功能驱动程序尝试重置和恢复有故障设备的标准方式。

### <a name="usb-1507"></a>USB

下面是 Windows 10 中 USB 的新增功能。 有关详细信息，请参阅 [Windows 10：USB 的新增功能](https://docs.microsoft.com/windows-hardware/drivers/usbcon/windows-10--what-s-new-for-usb)。

* 根据 USB 3.1 规范中的定义原生支持 USB 类型 C。 如果使用 USB 类型 C 连接器生成系统，可以使用现成的 [USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)或[编写 USB 类型 C 连接器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)。
* 双重角色功能使移动设备（例如手机、平板手机或平板电脑）可将自身指定为设备或主机。   有关详细信息，请参阅 [USB 双重角色驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-dual-role-driver-stack-architecture)。
* 支持使用 [Microsoft 提供的 USB 设备模拟类扩展 (UdeCx)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/system-supplied-usb-drivers) 编写 USB 模拟设备的驱动程序。
* 支持为不符合 xHCI 规范的主控制器或者为虚拟主控制器编写驱动程序。 若要编写此类驱动程序，请参阅[为 USB 主控制器开发 Windows驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/developing-windows-drivers-for-usb-host-controllers)。
* 支持使用 USB 功能类扩展 (UFX) 编写功能控制器驱动程序。 请参阅[为 USB 功能控制器开发 Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/developing-windows-drivers-for-usb-function-controllers)。

### <a name="wlan-1507"></a>WLAN

WDI（WLAN 设备驱动程序接口）是一个新的 [WLAN 通用 Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/network/wifi-universal-driver-model)，可在 Windows 10 桌面版和 Windows 10 移动版上融合 WLAN 驱动程序。

[返回页首](#top)

## <a name="deprecated-features"></a>已弃用的功能

下表描述了 Windows 10 中已删除的 Windows 驱动程序开发功能。

| 驱动程序技术 | 功能 | 弃用该功能的版本 |
|---|---|---|
| GNSS/定位 | [Windows 8.1 的地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)和相关文档 | Windows 10 版本 1709 |
| 移动运营商方案（网络） | [AllowStandardUserPinUnlock](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/allowstandarduserpinunlock) | Windows 10 版本 1709 |
| 扫描/成像 | [WSD（设备 Web 服务）质询器](https://docs.microsoft.com/windows-hardware/drivers/image/challenging-a-disconnected-scanner-with-the-wsd-challenger)功能和相关文档 | Windows 10 版本 1709 |
|移动运营商| 由于 MO UWP APPS 和 COSA 的推出，包含 Sysdev 元数据包的移动宽带应用体验已弃用。 | Windows 10 版本 1803|
