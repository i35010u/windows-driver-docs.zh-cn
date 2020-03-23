---
title: Windows 中的 USBView
description: USBView
ms.assetid: 88d2a93f-2e7c-493c-bb9e-487f1d1f2016
keywords:
- USBView
ms.date: 02/22/2017
ms.localizationpriority: high
ms.openlocfilehash: 54ba17767e3bd70a172d1dea99322990fcbd8812
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335953"
---
# <a name="usbview"></a>USBView

通用串行总线查看器 (USBView)（即 USBView.exe）是一种 Windows 图形 UI 应用，可用于浏览计算机上的所有 USB 控制器和连接的 USB 设备。 USBView 适用于所有版本的 Windows。

## <a name="span-idwhere_to_get_usbviewspanspan-idwhere_to_get_usbviewspanspan-idwhere_to_get_usbviewspanwhere-to-get-usbview"></a><span id="Where_to_get_USBView"></span><span id="where_to_get_usbview"></span><span id="WHERE_TO_GET_USBVIEW"></span>从何处获取 USBView

若要下载和使用 USBView，请完成以下步骤：

1. [下载并安装 Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

2. 在安装过程中，仅选择“Windows 调试工具”框，然后清除所有其他框  。

3. 默认情况下，在 x64 电脑上，SDK 将 USBView 安装到以下目录中。

   `C:\Program Files (x86)\Windows Kits\10\Debuggers\x64`

4. 打开正在运行的处理器类型的工具包调试程序目录，然后选择 USBView.exe 以启动该实用工具。


## <a name="usbview-source-code"></a>USBView 源代码

GitHub 上的 [Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中也提供了 [USBView](https://go.microsoft.com/fwlink/p/?LinkId=618004)。

## <a name="span-idusing_usbviewspanspan-idusing_usbviewspanuse-usbview"></a><span id="using_usbview"></span><span id="USING_USBVIEW"></span>使用 USBView


USBView 可以枚举 USB 主机控制器、USB 集线器和连接的 USB 设备。 它还可以从注册表中以及通过对设备的 USB 请求查询有关设备的信息。

主 USBView 窗口包含两个窗格。 左窗格显示了一个面向连接的树视图，你可以使用它来选择任何 USB 设备。

右窗格显示与所选 USB 设备有关的 USB 数据结构。 这些结构包括设备、配置、接口和终结点描述符以及当前设备配置。


## <a name="use-device-manager-to-display-usb-info"></a>使用设备管理器显示 USB 信息

若要使用设备管理器显示 USB 信息，请执行以下操作：

1. 选择 Windows 徽标键+R，在弹出框中输入“devmgmt.msc”，然后选择 Enter  。

2. 在设备管理器中，选择你的计算机，使其突出显示。

3. 选择“操作”，然后选择“扫描硬件更改”   。

4. 选择“查看”，然后选择“隐藏的设备”以显示其他设备（例如当前未处于活动状态的设备）   。 

5. 在设备管理器中展开“通用串行总线控制器”节点，然后选择所讨论的设备  。

7. 右键单击以选择“属性”并查看摘要设备状态信息  。

8. 选择“详细信息”选项卡查看其他信息  。 

9. 选择“属性”以查看详细信息，例如“状态”或“问题代码”    。


## <a name="windows-usb-troubleshooter"></a>Windows USB 疑难解答

如果尝试使用“安全删除硬件”对话框来诊断无法弹出的 USB 设备，请尝试使用 [Windows USB 疑难解答](https://support.microsoft.com/help/17614/windows-10-troubleshoot-common-usb-problems)  。


 

 





