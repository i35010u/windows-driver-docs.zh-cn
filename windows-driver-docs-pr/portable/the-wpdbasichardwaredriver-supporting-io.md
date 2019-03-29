---
Description: Supporting I/O
title: 支持 I/O
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798e00df7061e57ca8f86d1bdc531b5a6a7c0993
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575155"
---
# <a name="supporting-io"></a>支持 I/O


示例驱动程序通过使用 RS 232 连接与视差基本戳微型控制器进行通信。

微型控制器进行编程，发送定期传感器读数和驱动程序更新的传输时间间隔中接收输入的命令。

下图显示了示例驱动程序和基本戳单元之间的数据流。 出于演示目的，基本戳固件使用一个非常简单的协议来更新传感器数据：

-   基本标记将多字节的数据包发送到的驱动程序，其中包括*n*-传感器读取和更新间隔为 5 个字节的字节数。 通过使用 SEROUT 命令，而无需终止 null 字符 ANSI 字符在传输数据。 更新间隔定义前下一步的数据包将发送，并具有默认值为 02000 （2 秒） 经过的毫秒数。
-   若要动态配置的更新间隔，示例驱动程序可以将 6 字节数据包中包含终止 null 字符的 ANSI 字符中的新更新间隔 (如 05000\\0)。 终止 null 字符是必需的基本戳程序以使用 SERIN 命令接收的数据。

![i/o 数据流](images/wpd_overview_new.png)

示例驱动程序在 UMDF 主机进程 (WUDF 关系图中) 中承载，并接收来自 WPD 应用程序的命令。 该驱动程序通过使用 UMDF 文件句柄 I/O 目标对象交换 RS 232 端口使用的数据。

I/O 目标管理和完成回调例程在 RS232Target 对象中实现，并包括以下步骤：

1.  在中初始化**WpdBaseDriver::Initialize**，驱动程序配置 RS 232 连接设置，使用默认端口为 COM1。 特定于 RS 232 的安装程序代码中实现**RS232Connection**对象。
2.  示例驱动程序连接到 COM1 通过调用**CreateFileW**若要获取的句柄 RS 232 端口。
3.  示例驱动程序将使用**IWDFFileHandleTargetFactory::CreateFileHandleTarget**若要创建的文件句柄基于 I/O 目标对象，并将其分配给已检索到的 COM1 在步骤 2 中的句柄。 此安装程序代码中实现**RS232Target::Create**方法。
4.  示例驱动程序创建 I/O 目标后，在启动 I/O 目标**IPnpCallback::OnDOEntry**通过调用**RS232Target::Start**。 如果目标是处理请求准备就绪，该驱动程序会将第一次异步读取的请求发送到它。 每当从要修改的更新间隔属性的应用程序收到命令时，该驱动程序还会发送异步写入请求。
5.  该驱动程序时 （例如，devnode 处于禁用状态的设备管理器中时），未初始化**IPnpCallback::OnD0Exit**调用，并且示例驱动程序将通过调用停止 I/O 目标**RS232Target::Stop**. 如果有任何挂起的 I/O 请求的目标，它们将自动取消 UMDF。

RS232 读取请求将执行以下步骤中所示：

1.  在中生成**RS232Target::SendReadRequest**作为**IWDFIoRequest**对象，
2.  使用进行初始化**IWDFIoTarget::FormatRequestForRead**，和
3.  通过使用转发**IWDFIoRequest::Send**。

**RS232Target::OnCompletion**回调例程处理的请求数据，并发送下一个读取请求。

以下列表中所示实现 RS232 写入请求：

1.  在中生成**RS232Target::SendWriteRequest**作为**IWDFIoRequest**对象，
2.  使用进行初始化**IWDFIoTarget::FormatRequestForWrite**，和
3.  通过使用转发**IWDFIoRequest::Send**。

当应用程序设置传感器\_更新\_间隔属性值**WpdObjectProperties::OnSetPropertyValues**命令处理程序会调用 helper 函数**WpdObjectProperties::SendUpdateIntervalToDevice**，而后者又会调用**RS232Target::SendWriteRequest**。

UMDF I/O 目标提供多项好处，包括状态管理和错误处理，并且会导致更简单且更可靠的驱动程序代码。 对于更高级的驱动程序方案或堆栈配置，UMDF I/O 目标也提供本机支持取消，请求排队，并请求转发到下一个较低的驱动程序。

示例驱动程序，请使用 UMDF 文件 – 基于句柄的 I/O 目标对象而不 Microsoft Win32® Api 时不会产生感知的性能开销。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





