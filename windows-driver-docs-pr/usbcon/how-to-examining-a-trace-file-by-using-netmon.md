---
Description: 本主题介绍如何为示例的事件跟踪文件使用网络监视器。
title: 如何在 Netmon 中查看 USB ETW 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26caa503bf8ed3601146c15c2f5e73db5ac6a888
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405044"
---
# <a name="how-to-view-a-usb-etw-trace-in-netmon"></a>如何在 Netmon 中查看 USB ETW 跟踪

本主题介绍如何为示例的事件跟踪文件使用网络监视器。

安装 Netmon 并将其配置为使用 USB ETW 的文件，如中所述后[如何安装 Netmon 和 USB ETW 分析程序](how-to-install-netmon-and-the-netmon-usb-parser.md)，可以使用它来检查跟踪文件。

## <a name="opening-an-etw-file"></a>打开 ETW 文件

若要查看跟踪文件中网络监视器，在开始屏幕上，键入"网络监视器"以打开网络监视器。 通过使用以下方法之一打开跟踪文件：

* 上**文件**菜单上，单击**打开**，单击**捕获**，然后选择.etl 文件。
* 单击**打开捕获**按钮，然后选择.etl 文件。
* 按 CTRL + O，并选择.etl 文件。

事件跟踪由单个事件，其中每个表示该驱动程序堆栈中所发生情况的部分组成。 每个事件符合定义的驱动程序堆栈的多个类型之一。

![microsoft 网络监视器](images/netmon-ui-intro.png)

观察中列出了事件**帧摘要**窗格。 上图显示了 evens 从 USB 2.0 驱动程序堆栈。 请注意此窗格中的以下列：

* **时间偏移量**:指定为从该日志的开始时间的偏移量的事件的时间戳。
* **协议名称**:记录事件驱动程序。 对于 USB 事件，该驱动程序是 USB 集线器或 USB 端口。
* 描述：事件的描述性名称。

选择中的事件**帧摘要**窗格。 Netmon 显示中的事件的详细信息**帧详细信息**并**Hex 详细信息**窗格。 在中**帧详细信息**窗格中，展开要检查的事件详细信息的项。
有关使用 Netmon 检查 USB 跟踪文件的示例，请参阅[案例研究：使用 ETW 和 Netmon 未知的 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)。

## <a name="new-columns-the-usb-etw-parser-for-usb-30-driver-stack"></a>新列 USB 3.0 驱动程序的 USB ETW 分析器堆栈

USB 3.0 驱动程序堆栈中还定义重要的 USB 2.0 驱动程序堆栈中的事件的类型。 但是，有这些类型之间的细微差异。 例如，考虑 USB 控制传输完成事件类型 (**说明**:USBPort： 完成 URB\_函数\_控制\_传输\_EX 与数据):

对于 USB 2.0 驱动程序堆栈事件类型，**帧详细信息**窗格会显示 idVendor (也称为 USB VID) 和 idProduct (也称为 USB PID)。 此图显示了连接到 USB 2.0 主控制器的 USB 2.0 设备的事件跟踪。

![microsoft 网络监视器](images/vid-pid-usb2-0.png)

对于 USB 3.0 驱动程序堆栈事件类型，**帧详细信息**窗格中未包含 idVendor 或 idPid。 信息是通过添加到新列可用**帧摘要**窗格此图中所示。

请注意，这些新的列：

* **USB 设备描述**
* **USB 视频**
* **USB Pid**
* **USB 长度**
* **USB 请求持续时间**

![microsoft 网络监视器](images/usb-3-netmon.png)

所有 USB 事件跟踪 （USB 2.0 和 USB 3.0） 现在显示有关请求的信息为每个 URB 完成。 注意，在值，例如"41 255" **USB 长度**。 这些值表示在完成每个 URB 的实际传输长度，总请求长度 (原始 TransferBufferLength 指定的客户端驱动程序) 的上下文。 另请参阅 （以秒为单位） 所用的时间下，完成的请求**USB 请求持续时间**列。

## <a name="adding-filters-to-the-display-filter-pane"></a>将筛选器添加到显示筛选器窗格

可以使用捕获筛选器以缩小特定方案的事件跟踪。 从 USB 2.0 和 USB 3.0 驱动程序堆栈，可以编写新的事件跟踪的筛选器：

```syntax
USBIsError == 1      // Any error events from the USB drivers
USBIsDisconnect == 1 // Show when any device disconnected
```

可以筛选的所有列。 若要创建筛选器，右键单击一个单元格，然后选择**添加"&lt;列名&gt;"显示筛选器到**。 Netmon 创建基于其值和列名称的筛选器，并将其下添加**显示筛选器**窗格。

## <a name="related-topics"></a>相关主题

[使用 USB ETW](using-usb-etw.md)  
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  
[案例研究：使用 ETW 和 Netmon 未知的 USB 设备进行故障排除](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)  
