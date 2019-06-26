---
title: 写入到系统事件日志
description: 写入到系统事件日志
ms.assetid: 19be8bb4-8736-4d1a-92e5-b63a5f04e254
keywords:
- NTSTATUS 值 WDK 内核
- 转储数据 WDK 内核
- 预定义的错误代码 WDK 内核
- 系统事件日志 WDK 内核
- 属性表 WDK 错误
- 事件查看器 WDK 内核
- 示例日志条目属性表 WDK 内核
- 日志条目 WDK 内核
- 条目 WDK 错误日志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0b61cd95a273450f777a86a71bd89d7fb4d63e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374101"
---
# <a name="writing-to-the-system-event-log"></a>写入到系统事件日志





错误由其 NTSTATUS 值指定。 在系统预定义了可以使用的驱动程序的特定 NTSTATUS 值和驱动程序编写人员可以定义其他错误。 请注意记录错误时，可以使用仅限特定 NTSTATUS 值。

记录错误时，可以使用每个 NTSTATUS 值具有相关联的错误消息。 例如，并行端口驱动程序使用 NTSTATUS 值 PAR\_中断\_冲突来表示硬件中断发生冲突，使用的消息文本"中断 %1 检测到冲突"。

事件查看器显示中的消息正文**说明**日志条目的属性表上的文本框。 如果消息的文本字符串中包含"%1"，事件查看器使用的设备记录该条目的名称替换它。 消息文本可以包含窗体"%2"，"%3"的其他参数，依此类推。 当驱动程序会将错误记录时，它可以为这些参数提供字符串值。 这些字符串值被称为*插入字符串*。 事件查看器会自动插入它们来替代百分比值。

该驱动程序还可以在日志条目中，名为包含二进制数据*转储数据*。 事件查看器显示在转储数据**数据**日志条目的属性表的文本框。

您可以打开日志条目的属性表通过双击该项在事件查看器。 下面的屏幕截图显示了示例日志条目属性表。

![事件属性表的屏幕截图](images/event-properties.png)

驱动程序使用[ **IoAllocateErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateerrorlogentry)例程来分配一个错误日志条目。 日志条目包含可变长度[ **IO\_错误\_日志\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_error_log_packet)标头后, 跟插入字符串。

下图显示了在内存中的错误日志项的布局。

![说明在内存中的错误日志数据包的布局的关系图 ](images/errorlogentry.png)

**ErrorCode**的成员**IO\_错误\_日志\_数据包**指定错误的 NTSTATUS 值。 **DumpData**成员指定的日志项的任何转储数据。 **DumpData**是可变的数组，通过指定其大小**DumpDataSize**成员。 驱动程序指定的第一个插入字符串的开头**StringOffset**成员和中的字符串数**NumberOfStrings**成员。 每个插入字符串本身是以 null 结尾的 Unicode 字符串。

后驱动程序填充分配的错误日志条目，它的项写入错误日志使用[ **IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)。 **IoWriteErrorLogEntry**自动释放为日志条目分配的内存。 驱动程序可以使用[ **IoFreeErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeerrorlogentry)以释放任何未使用的日志条目。

预定义的错误代码 (窗体 IO\_ERR\_*XXX*) ntiologc.h 标头文件包含使用 Windows Driver Kit (WDK) 中定义。 可以 ntiologc.h 旁边的错误代码的声明的注释中找到与每个错误代码关联的错误消息。 若要使用预定义的错误代码，该驱动程序必须将系统文件，iologmsg.dll，注册为相关联的错误消息的源。 有关详细信息，请参阅[注册为错误消息源](registering-as-a-source-of-error-messages.md)。

驱动程序还可以定义他们自己的自定义错误类型和相关的错误消息。 有关详细信息，请参阅[定义自定义错误类型](defining-custom-error-types.md)。

 

 




