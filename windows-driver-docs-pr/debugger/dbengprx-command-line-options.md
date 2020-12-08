---
title: DbEngPrx 命令行选项
description: DbEngPrx 命令行使用以下语法。
keywords:
- DbEngPrx Command-Line 选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbEngPrx Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6260f5e9b7c3cdd427e434df91074c23c0b31a5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783539"
---
# <a name="dbengprx-command-line-options"></a>DbEngPrx 命令行选项


DbEngPrx 命令行使用以下语法。

```dbgcmd
dbengprx [-p] -c ClientTransport -s ServerTransport 

dbengprx -? 
```

## <a name="span-idddk_dbengprx_command_line_options_dbgspanspan-idddk_dbengprx_command_line_options_dbgspanparameters"></a><span id="ddk_dbengprx_command_line_options_dbg"></span><span id="DDK_DBENGPRX_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-p______"></span><span id="_______-P______"></span>**-p**   
导致 DbEngPrx 在删除所有连接后继续现有。

<span id="_______-c_______ClientTransport______"></span><span id="_______-c_______clienttransport______"></span><span id="_______-C_______CLIENTTRANSPORT______"></span>**-c** *ClientTransport*   
指定要在连接到服务器时使用的协议设置。 协议应与创建服务器时使用的协议匹配。 有关详细信息，请参阅 [**激活中继器**](activating-a-repeater.md)。

<span id="_______-s_______ServerTransport______"></span><span id="_______-s_______servertransport______"></span><span id="_______-S_______SERVERTRANSPORT______"></span>**-s** *ServerTransport*   
指定将在客户端连接到中继器时使用的协议设置。 有关详细信息，请参阅 [**激活中继器**](activating-a-repeater.md)。

<span id="_______-_______"></span> **-?**   
显示包含 DbEngPrx 命令行帮助文本的消息框。

有关使用 DbEngPrx 的信息，请参阅 [中继器](repeaters.md)。

 

 





