---
description: 本主题说明如何使用 Netmon 来举例说明如何使用事件跟踪文件。
title: 如何在 Netmon 中查看 USB ETW 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0024c7a4b8866d0d7428457afbc322601007d227
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662415"
---
# <a name="how-to-view-a-usb-etw-trace-in-netmon"></a>如何在 Netmon 中查看 USB ETW 跟踪

本主题说明如何使用 Netmon 来举例说明如何使用事件跟踪文件。

安装 Netmon 并将其配置为与 USB ETW 文件一起使用时，如 [如何安装 Netmon 和 USB Etw 分析器](how-to-install-netmon-and-the-netmon-usb-parser.md)中所述，你可以使用它来检查跟踪文件。

## <a name="opening-an-etw-file"></a>打开 ETW 文件

若要在 Netmon 中查看跟踪文件，请在 "开始" 屏幕上键入 "netmon" 以打开 Netmon。 使用以下方法之一打开跟踪文件：

* 在 " **文件** " 菜单上，单击 " **打开**"，单击 " **捕获**"，然后选择 .etl 文件。
* 单击 " **打开捕获** " 按钮，然后选择 .etl 文件。
* 按 CTRL + O 并选择 .etl 文件。

事件跟踪由单个事件组成，每个事件都指示驱动程序堆栈中发生的情况。 每个事件都符合驱动程序堆栈定义的多种类型中的一种。

![屏幕截图，显示 "Netmon" 窗口，其中包含在 "帧摘要" 中选择的事件。](images/netmon-ui-intro.png)

观察 " **帧摘要** " 窗格中列出的事件。 上图显示了来自 USB 2.0 驱动程序堆栈的能够。 注意此窗格中的以下各列：

* **时间偏移量**：事件的时间戳，指定为日志开始时间的偏移量。
* **协议名称**：记录事件的驱动程序。 对于 USB 事件，驱动程序为 USB 集线器或 USB 端口。
* **说明**：事件的描述性名称。

在 " **帧摘要** " 窗格中选择一个事件。 Netmon 在 " **帧详细信息** " 和 " **十六进制详细信息** " 窗格中显示事件的详细信息。 在 " **帧详细信息** " 窗格中，展开项以检查事件的详细信息。
有关使用 Netmon 检查 USB 跟踪文件的示例，请参阅 [案例研究：使用 ETW 和 Netmon 排查未知 USB 设备问题](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)。

## <a name="new-columns-the-usb-etw-parser-for-usb-30-driver-stack"></a>新列 USB 3.0 驱动程序堆栈的 USB ETW 分析器

Usb 2.0 驱动程序堆栈中的重要事件类型也是在 USB 3.0 驱动程序堆栈中定义的。 但是，这两种类型之间存在细微的差异。 例如，考虑 USB 控件传输完成事件类型 (**说明** ： USBPort： Complete URB \_ 函数 \_ 控制 \_ 传输 \_ ，例如数据) ：

对于 USB 2.0 驱动程序堆栈事件类型，" **帧详细信息** " 窗格显示 idVendor (也称为 usb VID) 和 idProduct (也称为 usb PID) 。 此图像显示连接到 USB 2.0 主机控制器的 USB 2.0 设备的事件跟踪。

![屏幕截图，显示 "Netmon" 窗口，其中包含连接到 "帧详细信息" 窗格中的 u b 主机控制器的 U B 设备的事件跟踪。](images/vid-pid-usb2-0.png)

对于 USB 3.0 驱动程序堆栈事件类型，" **帧详细信息** " 窗格不包含 IdVendor 或 idPid。 可以通过将新列添加到 " **帧摘要** " 窗格中来获取该信息，如图所示。

请注意以下新列：

* **USB 设备描述**
* **USB Vid**
* **USB Pid**
* **USB 长度**
* **USB 请求持续时间**

![microsoft 网络监视器](images/usb-3-netmon.png)

 (USB 2.0 和 USB 3.0) 的所有 USB 事件跟踪现在会在每个 URB 完成时显示有关请求的详细信息。 请注意，在 " **USB 长度**" 下的值为 "41 of 255"。 这些值指示每个 URB 完成时的实际传输长度，其中包含客户端驱动程序) 指定的请求总长度 (原始 TransferBufferLength 的上下文。 此外，还可以查看 " **USB 请求持续时间** " 列下请求完成所用的时间长度（以秒为单位）)  (。

## <a name="adding-filters-to-the-display-filter-pane"></a>将筛选器添加到 "显示筛选器" 窗格

您可以使用捕获筛选器来缩小特定方案的事件跟踪。 可以从 USB 2.0 和 USB 3.0 驱动程序堆栈为事件跟踪编写新的筛选器：

```syntax
USBIsError == 1      // Any error events from the USB drivers
USBIsDisconnect == 1 // Show when any device disconnected
```

所有列都可以进行筛选。 若要创建筛选器，请右键单击某个单元，然后选择 **" &lt; 列名称 &gt; " 以显示筛选器**。 Netmon 基于其值和列名创建筛选器，并将其添加到 " **显示筛选器** " 窗格下。

## <a name="related-topics"></a>相关主题

[使用 USB ETW](using-usb-etw.md)  
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
[案例研究：使用 ETW 和 Netmon 排查未知 USB 设备的问题](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)  
