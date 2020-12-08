---
title: 跟踪消息列表列
description: 跟踪消息列表列
keywords:
- 跟踪消息列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c10d5252cafdd87708b240a42d270c71d89f89df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840403"
---
# <a name="trace-message-list-columns"></a>跟踪消息列表列


跟踪消息列表中的列表示跟踪消息的属性，这类似于通常出现在 [跟踪消息前缀](trace-message-prefix.md)中的属性。 您可以显示和隐藏列，但不能对它们重新排序。

默认情况下，" **ID** " 字段和以下列表中描述的前八列都显示在跟踪消息列表中。 有关选择要显示的列的详细信息，请参阅显示和隐藏列。

<span id="ID"></span><span id="id"></span>**识别**  
**ID** 显示在跟踪消息列表窗口框架中。 它显示跟踪会话的 *组 ID* 、TraceView 分配给跟踪会话和跟踪会话组的标识符。 **组 ID** 还会显示在 "[跟踪会话" 列表](trace-session-list.md)的第一列中，以帮助你将跟踪会话与其跟踪消息相关联。

<span id="Msg_"></span><span id="msg_"></span><span id="MSG_"></span>**缺少\#**  
显示跟踪消息的消息号。 默认情况下，跟踪消息列表按 "**消息 \#** " 列中的值进行排序。

<span id="Name"></span><span id="name"></span><span id="NAME"></span>**路径名**  
显示跟踪消息的 [消息 GUID](message-guid.md) 的友好名称。 默认情况下，消息 GUID 的友好名称是在其中生成跟踪提供程序的目录的名称。

对于 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，此列显示生成消息 (内核跟踪子组件的名称，例如 "FileIo" ) 。

您可以使用 RUN WPP 或 Tracewpp 的 **-p** 参数 \_ ，为消息 GUID 的友好名称指定替换值。 有关信息，请参阅运行 \_ WPP 选项。

<span id="Process_ID"></span><span id="process_id"></span><span id="PROCESS_ID"></span>**进程 ID**  
标识生成跟踪消息的进程。

<span id="Thread_ID"></span><span id="thread_id"></span><span id="THREAD_ID"></span>**线程 ID**  
标识生成跟踪消息的线程。

<span id="CPU_"></span><span id="cpu_"></span>**CPU\#**  
标识生成跟踪消息的 CPU。

<span id="Sequence_"></span><span id="sequence_"></span><span id="SEQUENCE_"></span>**按\#**  
显示跟踪消息的本地序列号或全局序列号。 仅在此跟踪会话中唯一的本地序列号是默认值。

<span id="System_Time"></span><span id="system_time"></span><span id="SYSTEM_TIME"></span>**系统时间**  
显示生成跟踪消息时的系统计时器值。 因为系统计时器的分辨率为10毫秒，所以多个事件的系统时间值可能相同。

<span id="Message"></span><span id="message"></span><span id="MESSAGE"></span>**消息**  
显示跟踪消息。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>**文件名**  
显示生成跟踪消息的源文件的名称。

<span id="Line__"></span><span id="line__"></span><span id="LINE__"></span>**内嵌 \#**  
显示生成跟踪消息的代码的行号。

<span id="Func_Name"></span><span id="func_name"></span><span id="FUNC_NAME"></span>**Func 名称**  
显示生成跟踪消息的函数的名称。

<span id="Kernel_Time"></span><span id="kernel_time"></span><span id="KERNEL_TIME"></span>**内核时间**  
显示生成跟踪消息时内核模式指令的已用执行时间（以 CPU 刻度为单位）。

<span id="User_Time"></span><span id="user_time"></span><span id="USER_TIME"></span>**用户时间**  
显示生成跟踪消息时用户模式指令的已用执行时间（以 CPU 刻度为单位）。

<span id="Indent"></span><span id="indent"></span><span id="INDENT"></span>**降低**  
显示在将跟踪消息写入文本日志时缩进的空格数。

<span id="Flags_Name"></span><span id="flags_name"></span><span id="FLAGS_NAME"></span>**标志名称**  
显示生成跟踪消息时为提供程序启用的 [跟踪标志](trace-flags.md) 的名称。

<span id="Level_Name"></span><span id="level_name"></span><span id="LEVEL_NAME"></span>**级别名称**  
显示生成跟踪消息时为提供程序启用的 [跟踪级别](trace-level.md) 的值。

<span id="Component_Name"></span><span id="component_name"></span><span id="COMPONENT_NAME"></span>**组件名称**  
显示生成跟踪消息的提供程序组件的名称。 仅当在跟踪代码中指定组件名称时，才会显示该组件名称。

<span id="SubComponent_Name"></span><span id="subcomponent_name"></span><span id="SUBCOMPONENT_NAME"></span>**子组件名称**  
显示生成跟踪消息的提供程序的子组件的名称。 仅当在跟踪代码中指定子组件名称时，才会显示子组件名称。

<span id="Save_As_Default"></span><span id="save_as_default"></span><span id="SAVE_AS_DEFAULT"></span>**另存为默认值**  
此选项不是列名称。 它是一个命令，用于将当前显示的列配置保存为将来跟踪会话的默认配置。 有关详细信息，请参阅 [跟踪消息列表功能](trace-message-list-features.md)中的 "保存列配置"。

 

 





