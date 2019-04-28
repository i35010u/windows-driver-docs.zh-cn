---
title: PoolMon 运行时命令
description: 若要更改显示 PoolMon 正在运行时，使用运行命令。
ms.assetid: 834f406d-5e5d-416e-90df-b52b61d70ea7
keywords:
- PoolMon 运行时的命令驱动程序开发工具
topic_type:
- apiref
api_name:
- PoolMon Run-time Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa05117519f0d8f87b20a32da6a03b346c2b305
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338694"
---
# <a name="poolmon-run-time-commands"></a>PoolMon 运行时命令


若要更改显示 PoolMon 正在运行时，使用运行命令。 每个运行时命令由单个键盘字符组成。 按密钥执行命令。

```
    [p] [( | )] [s] [TSSessionID] [i] [l] [e] [t] [a] [f] [d] [b] [m] [h | ?] [q | ESC]
```

## <a name="span-idddkpoolmonruntimecommandstoolsspanspan-idddkpoolmonruntimecommandstoolsspanparameters"></a><span id="ddk_poolmon_run_time_commands_tools"></span><span id="DDK_POOLMON_RUN_TIME_COMMANDS_TOOLS"></span>参数


<span id="_______p______"></span><span id="_______P______"></span> **p**   
切换通过非分页的分配、 分页的分配和同时显示。

<span id="_________or__"></span><span id="_________OR__"></span> **(** 或 **)**  
切换显示之间排序的值 （分配、 可用操作和字节数） 和按值中的更改进行排序。 可以使用任一括号字符。 它们具有相同的效果。

<span id="_______s______"></span><span id="_______S______"></span> **s**   
切换系统池和终端服务会话池之间显示。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span> *TSSessionID*   
显示从指定的终端服务会话池分配。 *TSSessionID*表示终端服务会话的会话 ID。 它必须是从 0 到 9 的整数。 若要显示所有会话池或输入的会话 Id 大于 9，请使用**我**命令。

<span id="_______i______"></span><span id="_______I______"></span> **i**   
提示你提供的终端服务器会话的会话 ID。 您可以响应下列两项操作：

-   若要显示从终端服务会话的所有池的分配，请按 ENTER。

-   若要显示从特定的终端服务会话池分配，键入一个会话 ID，然后按 ENTER。

<span id="_______l______"></span><span id="_______L______"></span> **l**   
切换打开和关闭更改过的行的突出显示。

<span id="_______e______"></span><span id="_______E______"></span> **e**   
切换打开和关闭池总计。 在显示的底部显示总计。

<span id="_______t______"></span><span id="_______T______"></span> **t**   
按标记名称排序。

<span id="_______a______"></span><span id="_______A______"></span> **a**   
按分配数排序。 与括号字符一起使用时键进行排序所分配的更改。

<span id="_______f______"></span><span id="_______F______"></span> **f**   
通过免费的操作数的排序。 与括号字符一起使用时**f**键进行排序的可用操作中的更改。

<span id="_______d______"></span><span id="_______D______"></span> **d**   
分配的字节数和释放的字节数之间的差异进行排序。

<span id="_______b______"></span><span id="_______B______"></span> **b**   
使用字节数按排序。 与括号字符一起使用时**b**键进行排序以字节为单位使用此更改。

<span id="_______m______"></span><span id="_______M______"></span> **m**   
按每个分配的字节数排序。 与括号字符一起使用时**m**密钥的字节数每个分配的更改进行排序。

<span id="_________or_h"></span><span id="_________OR_H"></span> **?** 或**h**  
显示启动命令参数、 运行命令和 PoolMon 显示的说明。 若要关闭显示帮助内容，请按 ESC 键。

<span id="_______q_or_ESC"></span><span id="_______q_or_esc"></span><span id="_______Q_OR_ESC"></span> **问题与解答**或**ESC**  
停止 PoolMon。









