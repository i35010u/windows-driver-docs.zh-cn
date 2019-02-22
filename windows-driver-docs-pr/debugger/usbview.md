---
title: USBView
description: USBView
ms.assetid: 88d2a93f-2e7c-493c-bb9e-487f1d1f2016
keywords:
- USBView
ms.date: 02/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfffcf440c5d834cd31df985827985ef026456e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554870"
---
# <a name="usbview"></a>USBView

USBView （通用串行总线查看器，USBView.exe） 是使您能够浏览所有 USB 控制器和连接您的计算机上的 USB 设备的 Windows 图形用户界面应用程序。 USBView 适用于所有版本的 Windows。

## <a name="span-idwheretogetusbviewspanspan-idwheretogetusbviewspanspan-idwheretogetusbviewspanwhere-to-get-usbview"></a><span id="Where_to_get_USBView"></span><span id="where_to_get_usbview"></span><span id="WHERE_TO_GET_USBVIEW"></span>从中获取 USBView

若要下载并使用 USBView，请完成以下步骤：

1. [下载并安装 Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

2. 安装过程中，选择只**有关 Windows 调试工具**框，并清除所有其他框。

3. 默认情况下，在 x64 上 PC SDK 将安装 USBView，到此目录。

   `C:\Program Files (x86)\Windows Kits\10\Debuggers\x64`

4. 导航到正在运行，并且单击 usbview.exe 以启动该实用工具的处理器类型的工具包调试程序目录。


## <a name="usbview-source-code"></a>USBView 源代码

[USBView](https://go.microsoft.com/fwlink/p/?LinkId=618004)也位于[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

## <a name="span-idusingusbviewspanspan-idusingusbviewspanusing-usbview"></a><span id="using_usbview"></span><span id="USING_USBVIEW"></span>使用 USBView


USBView 可以枚举 USB 主控制器、 USB 集线器和附加的 USB 设备。 它还可以查询有关注册表中和通过 USB 请求到的设备的设备的信息。

主 USBView 窗口包含两个窗格。 左窗格中显示的面向连接的树视图中，使您可以选择任何 USB 设备。

右窗格显示属于所选的 USB 设备的 USB 数据结构。 这些结构包括设备、 配置、 接口和终结点描述符，以及当前的设备配置。


## <a name="using-device-manager-to-display-usb-information"></a>使用设备管理器来显示 USB 信息

若要使用 Windows 设备管理器显示 USB 信息：

1. 键入 Windows 键 + R，并在输入`devmgmt.msc`到弹出框，并按 Enter 键。

2. 在设备管理器中，单击您的计算机，以便它被突出显示。

3. 单击**操作**，然后单击**扫描检测硬件改动**。

4. 选择**视图**，然后单击**隐藏的设备**以显示其他设备，例如那些不是当前处于活动状态。 

5. 展开*通用串行总线控制器*节点在设备管理器。

6. 定位设备有问题，例如*USB 大容量存储设备*。

7. 右键单击该设备，然后选择**属性**查看摘要设备状态信息。

8. 单击**详细信息**选项卡以查看其他信息。 

9. 使用**属性**下拉框，以查看所需的信息，例如*状态*或*问题代码*。


## <a name="windows-usb-troubleshooter"></a>Windows USB 疑难解答

如果想要诊断不弹出使用安全删除硬件对话框中的 USB 设备，你可能想要尝试[Windows USB 疑难解答](https://support.microsoft.com/help/17614/automatically-diagnose-and-fix-windows-usb-problems)。


 

 





