---
title: 跟踪消息列表列
description: 跟踪消息列表列
ms.assetid: d0f5873e-9b01-4a74-8448-90194545da1f
keywords:
- 跟踪消息列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52726498ccf71f138fe65b79af67e3a1875ff629
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354633"
---
# <a name="trace-message-list-columns"></a>跟踪消息列表列


跟踪消息列表中的列表示的跟踪消息属性，类似于，通常会出现在[跟踪消息前缀](trace-message-prefix.md)。 您可以显示和隐藏的列，但你不能对其重新排序。

默认情况下**ID**字段和下面的列表中所述的前八列显示在跟踪消息列表。 有关选择要显示的列的详细信息，请参阅显示和隐藏列。

<span id="ID"></span><span id="id"></span>**ID**  
**ID**出现在跟踪消息列表的窗口框架。 它将显示*组 ID*跟踪会话的标识符的 TraceView 将分配给跟踪会话和跟踪会话组。 **组 ID**也会出现在第一列[跟踪会话列表](trace-session-list.md)以帮助您跟踪会话相关联其跟踪消息。

<span id="Msg_"></span><span id="msg_"></span><span id="MSG_"></span>**消息\#**  
显示的跟踪消息的消息数。 默认情况下，跟踪消息列表进行排序中的值**Msg\#** 列。

<span id="Name"></span><span id="name"></span><span id="NAME"></span>**名称**  
显示的友好名称[消息 GUID](message-guid.md)的跟踪消息。 默认情况下，消息 GUID 的友好名称是目录的在其中生成跟踪提供程序的名称。

有关[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，此列显示的生成消息 (例如，"FileIo") 的内核跟踪子组件名称。

可以使用 **-p**参数运行\_WPP 或 Tracewpp 指定备用值消息的 GUID 的友好名称。 有关信息，请参阅运行\_WPP 选项。

<span id="Process_ID"></span><span id="process_id"></span><span id="PROCESS_ID"></span>**Process ID**  
标识生成的跟踪消息的进程。

<span id="Thread_ID"></span><span id="thread_id"></span><span id="THREAD_ID"></span>**线程 ID**  
标识生成的跟踪消息的线程。

<span id="CPU_"></span><span id="cpu_"></span>**CPU\#**  
标识在其生成的跟踪消息的 CPU。

<span id="Sequence_"></span><span id="sequence_"></span><span id="SEQUENCE_"></span>**序列\#**  
显示跟踪消息的本地或全局序列号。 本地序列号，是仅对此跟踪会话唯一的这是默认值。

<span id="System_Time"></span><span id="system_time"></span><span id="SYSTEM_TIME"></span>**系统时间**  
显示系统计时器值时生成的跟踪消息。 由于系统计时器的分辨率为 10 毫秒，多个事件可以具有相同的系统时间值。

<span id="Message"></span><span id="message"></span><span id="MESSAGE"></span>**消息**  
显示跟踪消息。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>**文件的名称**  
显示生成的跟踪消息的源文件的名称。

<span id="Line__"></span><span id="line__"></span><span id="LINE__"></span>**行 \#**  
显示生成的跟踪消息的代码的行号。

<span id="Func_Name"></span><span id="func_name"></span><span id="FUNC_NAME"></span>**函数名称**  
显示生成的跟踪消息的函数的名称。

<span id="Kernel_Time"></span><span id="kernel_time"></span><span id="KERNEL_TIME"></span>**内核时间**  
在生成的跟踪消息的时间中 CPU 时钟周期数，显示内核模式的说明，已用的执行时间。

<span id="User_Time"></span><span id="user_time"></span><span id="USER_TIME"></span>**用户时间**  
在生成的跟踪消息的时间中 CPU 时钟周期数，显示用户模式下的说明，已用的执行时间。

<span id="Indent"></span><span id="indent"></span><span id="INDENT"></span>**缩进**  
显示跟踪消息写入到文本日志时是缩进的空格数。

<span id="Flags_Name"></span><span id="flags_name"></span><span id="FLAGS_NAME"></span>**标志名称**  
显示的名称[跟踪标志](trace-flags.md)时生成的跟踪消息的已启用提供程序。

<span id="Level_Name"></span><span id="level_name"></span><span id="LEVEL_NAME"></span>**级别名称**  
显示的值[跟踪级别](trace-level.md)已启用的提供程序时生成的跟踪消息。

<span id="Component_Name"></span><span id="component_name"></span><span id="COMPONENT_NAME"></span>**组件名称**  
显示生成的跟踪消息的提供程序的组件的名称。 仅当指定的跟踪代码中，将显示该组件名称。

<span id="SubComponent_Name"></span><span id="subcomponent_name"></span><span id="SUBCOMPONENT_NAME"></span>**子组件名称**  
显示生成的跟踪消息的提供程序的子组件名称。 仅当指定的跟踪代码中，将显示子组件名称。

<span id="Save_As_Default"></span><span id="save_as_default"></span><span id="SAVE_AS_DEFAULT"></span>**将另存为默认值**  
此选项不是列名称。 它是一个将当前显示的列配置为默认值保存为未来的跟踪会话的命令。 有关详细信息，请参阅 》 中"保存列配置"[跟踪消息列表功能](trace-message-list-features.md)。

 

 





