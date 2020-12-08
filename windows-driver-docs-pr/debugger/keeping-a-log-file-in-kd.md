---
title: 在 KD 中保存日志文件
description: 在 KD 中保存日志文件
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 238cab9ccf93c733e3e2af157ae6e677a5604624
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801919"
---
# <a name="keeping-a-log-file-in-kd"></a>在 KD 中保存日志文件


## <span id="ddk_keeping_a_log_file_dbg"></span><span id="DDK_KEEPING_A_LOG_FILE_DBG"></span>


KD 可以编写记录调试会话的日志文件。 此日志文件包含你键入的所有命令和来自调试器的响应。

### <a name="span-idopening_a_new_log_filespanspan-idopening_a_new_log_filespanopening-a-new-log-file"></a><span id="opening_a_new_log_file"></span><span id="OPENING_A_NEW_LOG_FILE"></span>打开新的日志文件

若要打开新的日志文件，或覆盖以前的日志文件，请执行以下操作之一：

-   在启动调试器之前，请设置 \_ NT \_ 调试 \_ 日志 \_ 文件 \_ 打开 [环境变量](environment-variables.md)。

-   启动调试器时，请使用 **-徽标** 命令行选项。

-   输入 " [**logopen (打开" 日志文件)**](-logopen--open-log-file-.md) "命令。 如果你使用 **/t** 选项，则日期和时间将追加到指定的文件名。 如果使用 **/u** 选项，则以 Unicode 而不是 ASCII 编写日志文件。

### <a name="span-idappending_to_an_existing_log_filespanspan-idappending_to_an_existing_log_filespanappending-to-an-existing-log-file"></a><span id="appending_to_an_existing_log_file"></span><span id="APPENDING_TO_AN_EXISTING_LOG_FILE"></span>追加到现有日志文件

若要将文本追加到现有日志文件，请执行以下操作之一：

-   在启动调试器之前，请设置 \_ NT \_ 调试 \_ 日志 \_ 文件 \_ 追加 [环境变量](environment-variables.md)。

-   启动调试器时，请使用 **-loga** 命令行选项。

-   输入 " [**logpath (追加日志文件)**](-logappend--append-log-file-.md) " 命令。 如果要追加到 Unicode 日志文件，必须使用 **/u** 选项。

### <a name="span-idclosing_a_log_filespanspan-idclosing_a_log_filespanclosing-a-log-file"></a><span id="closing_a_log_file"></span><span id="CLOSING_A_LOG_FILE"></span>关闭日志文件

若要关闭打开的日志文件，请执行以下操作：

-   输入 [**logclose (关闭日志文件)**](-logclose--close-log-file-.md) 命令。

### <a name="span-idchecking_log_file_statusspanspan-idchecking_log_file_statusspanchecking-log-file-status"></a><span id="checking_log_file_status"></span><span id="CHECKING_LOG_FILE_STATUS"></span>正在检查日志文件状态

若要确定日志文件的状态，请执行以下操作：

-   输入 [**logfile (显示 "日志文件状态")**](-logfile--display-log-file-status-.md) 命令。

 

 





