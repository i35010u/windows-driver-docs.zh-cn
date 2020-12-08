---
title: BinPlace 宏和环境变量
description: BinPlace 宏和环境变量
keywords:
- BinPlace WDK，环境变量
- 环境变量 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b7b6a00dbdfc4508c9cc7f8d4459d9ec572a90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794005"
---
# <a name="binplace-macros-and-environment-variables"></a>BinPlace 宏和环境变量


## <span id="ddk_binplace_environment_variables_tools"></span><span id="DDK_BINPLACE_ENVIRONMENT_VARIABLES_TOOLS"></span>


BinPlace 读取以下宏和环境变量的值：

<span id="BINPLACE_OVERRIDE_FLAGS"></span><span id="binplace_override_flags"></span>BINPLACE \_ 重写 \_ 标志  
指定包含其他命令行参数的文件。 BinPlace 将使用这些开关以及实际的命令行上的开关。 此替代文件中的开关将在实际的命令行开关之前进行分析。

<span id="________BINPLACE_LOG_______"></span><span id="________binplace_log_______"></span> BINPLACE \_ 日志   
指定日志文件的路径和文件名。 所有 BinPlace 操作都将记录在此日志文件中。

<span id="BINPLACE_MESSAGE_LOG"></span><span id="binplace_message_log"></span>BINPLACE \_ 消息 \_ 日志  
指定消息日志文件的路径和文件名。 每次执行 BinPlace 时，都会在消息日志文件中记录其命令行。 如果命令行使用前缀为 at 符号 ( ) 的文件展开 **@** ，则展开的命令行文本将存储在消息日志中。 但是， \_ \_ 将不会在消息日志文件中记录源自 BINPLACE OVERRIDE 标志文件的参数。

<span id="BINPLACE_EXCLUDE_FILE"></span><span id="binplace_exclude_file"></span>BINPLACE \_ 排除 \_ 文件  
指定排除文件的路径和文件名。 如果此值不存在，则默认值为 \\ tools \\symbad.txt。 SymChk 将使用此文件，就像它是 SymChk 的 **/ea** 开关的参数一样。  (SymChk 是 Windows 包调试工具的一部分。 有关详细信息，请参阅 [Windows 调试](../debugger/index.md) 。 ) 

<span id="TRACE_FORMAT_PATH"></span><span id="trace_format_path"></span>跟踪 \_ 格式 \_ 路径  
指定使用 **-： TMF** 开关时用于跟踪格式文件的路径。

<span id="_________NTTREE_______"></span><span id="_________nttree_______"></span>\_NTTREE   
指定在未使用 **-r** 开关的情况下，将在其中放置所有文件的根目标目录。 有关详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md)。

 

