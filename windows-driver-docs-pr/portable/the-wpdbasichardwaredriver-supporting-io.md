---
description: 支持 I/O
title: 支持 I/O
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d001a8c6475e03427154f7f2802febfab74b41b7
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969172"
---
# <a name="supporting-io"></a>支持 I/O


示例驱动程序通过使用 RS 232 连接与视差基本戳记微控制器进行通信。

微控制器被设计为发送定期传感器读数，并从驱动程序接收输入命令以更新传输间隔。

下图显示了示例驱动程序和基本戳记单元之间的数据流。 出于演示目的，基本戳记固件使用非常简单的协议来更新传感器数据：

-   基本戳记将多字节数据包发送到驱动程序，该驱动程序由 *n*个字节表示传感器读数，5个字节用于更新间隔。 数据通过使用 SEROUT 命令（不包含终止 null 字符）以 ANSI 字符传输。 更新间隔定义了发送下一个数据包前经过的毫秒数，默认值为 02000 (2 秒) 。
-   若要动态配置更新间隔，示例驱动程序可以发送一个6字节数据包，其中包含以 ANSI 字符表示的新更新间隔，其中包含终止 null 字符 (例如 05000 \\ 0) 。 基本戳记程序需要终止 null 字符，才能使用 SERIN 命令接收数据。

![i/o 数据流](images/wpd_overview_new.png)

示例驱动程序在) 关系图中 (WUDF 的 UMDF 主机进程中托管，并从 WPD 应用程序中接收命令。 驱动程序通过使用 UMDF 文件句柄 i/o 目标对象将数据与 RS 232 端口交换。

I/o 目标管理和完成回调例程是在 RS232Target 对象中实现的，包括以下步骤：

1.  在 **WpdBaseDriver：： Initialize**中初始化时，驱动程序将使用 COM1 作为默认端口配置 RS 232 连接设置。 在 **rs232connection.cpp** 对象中实现了特定于 RS 232 的安装代码。
2.  示例驱动程序通过调用 **CreateFileW** 以获取 RS 232 端口的句柄来连接到 COM1。
3.  示例驱动程序使用 **IWDFFileHandleTargetFactory：： CreateFileHandleTarget** 创建一个基于文件句柄的 i/o 目标对象，并将其分配给在步骤2中为 COM1 检索到的句柄。 此安装代码是在 **RS232Target：： Create** 方法中实现的。
4.  创建 i/o 目标后，示例驱动程序会通过调用**RS232Target：： Start**在**IPnpCallback：： OnDOEntry**中启动 i/o 目标。 如果目标已准备好处理请求，则驱动程序将向其发送第一个异步读取请求。 当驱动程序收到来自应用程序的命令来修改更新间隔属性时，它还会发送一个异步写入请求。
5.  如果驱动程序未初始化 (例如，在设备管理器) 中禁用 devnode 时，将调用 **IPnpCallback：： OnD0Exit** ，并且示例驱动程序将通过调用 **RS232Target：： stop**来停止 i/o 目标。 如果对目标有任何挂起的 i/o 请求，则该请求将被 UMDF 自动取消。

应按照以下步骤所示实现 RS232 读取请求：

1.  它们在 **RS232Target：： SendReadRequest** 中生成为 **IWDFIoRequest** 对象。
2.  使用 **IWDFIoTarget：： FormatRequestForRead**初始化它们，并
3.  使用 **IWDFIoRequest：： Send**转发它们。

**RS232Target：： OnCompletion**回调例程处理请求数据并发送下一个读取请求。

将实现 RS232 写入请求，如以下列表所示：

1.  它们在 **RS232Target：： SendWriteRequest** 中生成为 **IWDFIoRequest** 对象。
2.  使用 **IWDFIoTarget：： FormatRequestForWrite**初始化它们，并
3.  使用 **IWDFIoRequest：： Send**转发它们。

当应用程序设置传感器 \_ 更新 \_ 间隔属性值时， **WpdObjectProperties：： OnSetPropertyValues** 命令处理程序会调用 helper 函数 **WpdObjectProperties：： SendUpdateIntervalToDevice**，后者又调用 **RS232Target：： SendWriteRequest**。

UMDF i/o 目标提供多种优势，包括状态管理和错误处理，并导致驱动程序代码更简单、更可靠。 对于更高级的驱动程序方案或堆栈配置，UMDF i/o 目标还会以本机方式支持取消、请求排队和请求转发到下一个较低版本的驱动程序。

对于示例驱动程序，使用基于 UMDF 文件句柄的 i/o 目标对象而不是 Microsoft Win32® Api 时，没有明显的性能开销。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





