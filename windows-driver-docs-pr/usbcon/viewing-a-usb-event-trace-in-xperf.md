---
description: 本主题介绍如何在 Xperf 中查看 USB 事件跟踪。
title: 在 Xperf 中查看 USB 事件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d61bba89ff79ac1a991035465ad4b28120f304ba
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969076"
---
# <a name="viewing-a-usb-event-trace-in-xperf"></a>在 Xperf 中查看 USB 事件跟踪


本主题介绍如何在 Xperf 中查看 USB 事件跟踪。

若要分析性能和计时问题，可以使用 Xperf 查看 USB 事件跟踪。 例如，如果你有一个名为 "Xperf" 的事件跟踪日志文件，并且已下载了工具，请发出以下命令来分析跟踪：

```cpp
xperf usb.etl
```

Xperf 以图形形式显示事件的视图。 初始视图是一个时间线视图，其中每个菱形表示此图像中的一个或多个事件。 菱形按事件提供程序进行颜色编码。

![windows 性能分析器-xperf](images/xperf.png)

时间线视图以图形方式显示事件活动的群集。 在图形视图中，可以很容易地以1秒的时间间隔来查看事件活动的周期性性质，因为此示例跟踪中的设备摘要事件之后，USB 大容量存储设备发生了 USB 传输请求。

可以将鼠标指针移动到时间线的各个部分并放大。 此图显示了在跟踪非常简单的设备摘要事件上进行的放大。

![windows 性能分析器-xperf](images/xperf1.png)

您可以在电子表格窗体中显示整个跟踪的事件摘要表，也可以仅在所选间隔内显示此图像中显示的时间间隔。

![windows 性能分析器-xperf](images/xperf2.png)

若要显示摘要表，请在 " **一般事件** " 屏幕中右键单击，然后选择 " **摘要表**"。

事件摘要表是一个功能非常强大的视图，因为您可以通过拖动列来对它们重新排序，并根据新的列顺序对事件进行透视。 为了使你能够专注于感兴趣的项，你可以展开或折叠具有相同排序顺序的项。

Netmon，Netmon 以比 Xperf 更具可读性的形式显示 USB 事件数据，而 Netmon 缺少 Xperf 时间线和表视图。 若要在特定的时间段内分析跟踪的事件，可以在 Xperf 与 Netmon 之间切换。

## <a name="related-topics"></a>相关主题
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
[将 Xperf 与 USB ETW 配合使用](using-xperf-with-usb-etw.md)  



