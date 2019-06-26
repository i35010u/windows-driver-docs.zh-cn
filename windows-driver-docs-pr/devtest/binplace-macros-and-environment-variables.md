---
title: BinPlace 宏和环境变量
description: BinPlace 宏和环境变量
ms.assetid: f990e132-f6d7-46e1-8c86-6ae3f0483bd5
keywords:
- BinPlace WDK、 环境变量
- 环境变量 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e9e5acd26f4097f1c270a786e17341710793ff4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371660"
---
# <a name="binplace-macros-and-environment-variables"></a>BinPlace 宏和环境变量


## <span id="ddk_binplace_environment_variables_tools"></span><span id="DDK_BINPLACE_ENVIRONMENT_VARIABLES_TOOLS"></span>


BinPlace 读取以下宏和环境变量的值：

<span id="BINPLACE_OVERRIDE_FLAGS"></span><span id="binplace_override_flags"></span>BINPLACE\_OVERRIDE\_FLAGS  
指定包含其他命令行参数的文件。 BinPlace 将使用这些开关，以及它们在实际的命令行上。 此替代文件中的开关将分析之前的实际命令行开关。

<span id="________BINPLACE_LOG_______"></span><span id="________binplace_log_______"></span> BINPLACE\_日志   
指定日志文件的路径和文件。 在此日志文件，将记录所有 BinPlace 操作。

<span id="BINPLACE_MESSAGE_LOG"></span><span id="binplace_message_log"></span>BINPLACE\_消息\_日志  
指定消息日志文件的路径和文件。 每次执行 BinPlace 时，将在消息日志文件中记录其命令行。 如果使用带有前缀的文件扩展命令行 at 符号 ( **@** )，将消息日志中存储的扩展的命令行文本。 但是，参数源自 BINPLACE\_重写\_标志文件将不记录消息日志文件中。

<span id="BINPLACE_EXCLUDE_FILE"></span><span id="binplace_exclude_file"></span>BINPLACE\_EXCLUDE\_FILE  
指定排除文件的路径和文件。 如果不存在，则默认值是\\工具\\symbad.txt。 此文件将由 SymChk，就好像 SymChk 的参数 **/ea**切换。 （SymChk 是有关 Windows 调试工具软件包的一部分。 请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)有关详细信息。)

<span id="TRACE_FORMAT_PATH"></span><span id="trace_format_path"></span>跟踪\_格式\_路径  
指定要用于跟踪的路径格式文件时 **-: TMF**使用开关。

<span id="_________NTTREE_______"></span><span id="_________nttree_______"></span> \_NTTREE   
指定如果所有文件将都放置在其中的根目标目录 **-r**不使用开关。 有关详细信息，请参阅[BinPlace 目标目录](binplace-destination-directories.md)。

 

 





