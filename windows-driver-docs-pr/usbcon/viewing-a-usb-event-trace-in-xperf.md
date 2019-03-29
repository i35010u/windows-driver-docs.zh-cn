---
Description: This topic describes how to view a USB event trace in Xperf.
title: 在 Xperf 中查看 USB 事件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0ea8ac02a35e7684a820d36c838c792f9b4638
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566163"
---
# <a name="viewing-a-usb-event-trace-in-xperf"></a>在 Xperf 中查看 USB 事件跟踪


本主题介绍如何在 Xperf 中查看 USB 事件跟踪。

若要分析的性能和计时问题，可以使用 Xperf 查看 USB 的事件跟踪。 例如，如果具有名为 usb.etl 事件跟踪日志文件，并且你已下载 Xperf 工具，发出以下命令以分析跟踪：

```cpp
xperf usb.etl
```

Xperf 以图形形式显示的事件的视图。 初始视图是时间线视图，其中每个菱形表示在此图中的一个或多个事件。 菱形是颜色编码，根据事件提供程序。

![windows 性能分析器-xperf](images/xperf.png)

时间线视图以图形方式呈现群集的事件活动。 在图形视图中，很容易就可以看出隔 1 秒的定期事件活动的性质，作为在此示例跟踪中的设备摘要事件后，出现了 USB 大容量存储设备的 USB 传输请求。

可以在时间线的各部分之间移动鼠标指针并放大。 此图显示了放大上发生的跟踪的最开头的设备摘要事件。

![windows 性能分析器-xperf](images/xperf1.png)

此图中所示，可以显示一个事件的摘要表，在电子表格形式中，整个跟踪或所选间隔。

![windows 性能分析器-xperf](images/xperf2.png)

若要显示的摘要表，请右键单击**泛型事件**屏幕上，然后选择**摘要表**。

事件摘要表是一个非常强大的视图，因为您可以拖动列来重新排序它们和视图数据透视表基于新的列顺序的事件。 若要使您能够专注于感兴趣的项，可以展开或折叠项具有相同的排序顺序。

Netmon 有时比 Xperf，可读性更强的窗体中显示 USB 事件数据，但 Netmon 缺少 Xperf 时间线和表视图。 若要在特定时间段内分析跟踪的事件，可以 Xperf 和 Netmon 之间进行切换。

## <a name="related-topics"></a>相关主题
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  
[使用 USB ETW 使用 Xperf](using-xperf-with-usb-etw.md)  



