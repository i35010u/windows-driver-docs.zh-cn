---
title: DbEngPrx 命令行选项
description: DbEngPrx 命令行使用以下语法。
ms.assetid: 3c0675a4-93f0-4aaa-9f33-9a45c48c1ff4
keywords:
- DbEngPrx 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbEngPrx Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1953578fa35e04c602c37dc70e07f8979ccd38aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374947"
---
# <a name="dbengprx-command-line-options"></a>DbEngPrx 命令行选项


DbEngPrx 命令行使用以下语法。

```dbgcmd
dbengprx [-p] -c ClientTransport -s ServerTransport 

dbengprx -? 
```

## <a name="span-idddkdbengprxcommandlineoptionsdbgspanspan-idddkdbengprxcommandlineoptionsdbgspanparameters"></a><span id="ddk_dbengprx_command_line_options_dbg"></span><span id="DDK_DBENGPRX_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
导致 DbEngPrx 继续现有即使与它的所有连接将被都删除。

<span id="_______-c_______ClientTransport______"></span><span id="_______-c_______clienttransport______"></span><span id="_______-C_______CLIENTTRANSPORT______"></span> **-c** *ClientTransport*   
指定要在连接到服务器中使用的协议设置。 与协议应匹配创建服务器时使用。 有关详细信息，请参阅[**激活 Repeater**](activating-a-repeater.md)。

<span id="_______-s_______ServerTransport______"></span><span id="_______-s_______servertransport______"></span><span id="_______-S_______SERVERTRANSPORT______"></span> **-s** *ServerTransport*   
指定客户端连接到 repeater 时将使用的协议设置。 有关详细信息，请参阅[**激活 Repeater**](activating-a-repeater.md)。

<span id="_______-_______"></span> **-?**   
显示具有 DbEngPrx 命令行帮助文本的消息框。

有关使用 DbEngPrx 信息，请参阅[重复字符](repeaters.md)。

 

 





