---
title: PoolMon 运行时命令
description: 若要在 PoolMon 正在运行时更改显示，请使用运行时命令。
keywords:
- PoolMon 运行时命令驱动程序开发工具
topic_type:
- apiref
api_name:
- PoolMon Run-time Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7bea77834a9c0327503709b698e92fcbf42a80d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841011"
---
# <a name="poolmon-run-time-commands"></a>PoolMon 运行时命令


若要在 PoolMon 正在运行时更改显示，请使用运行时命令。 每个运行时命令都包含单个键盘字符。 按键以执行命令。

```
    [p] [( | )] [s] [TSSessionID] [i] [l] [e] [t] [a] [f] [d] [b] [m] [h | ?] [q | ESC]
```

## <a name="span-idddk_poolmon_run_time_commands_toolsspanspan-idddk_poolmon_run_time_commands_toolsspanparameters"></a><span id="ddk_poolmon_run_time_commands_tools"></span><span id="DDK_POOLMON_RUN_TIME_COMMANDS_TOOLS"></span>参数


<span id="_______p______"></span><span id="_______P______"></span>**p**   
通过非分页分配和/或分页分配来切换显示。

<span id="_________or__"></span><span id="_________OR__"></span>**(** 或 **)**  
在按值排序 (分配、自由操作和) 字节之间切换显示，并按值的更改进行排序。 可以使用括号字符。 它们具有相同的效果。

<span id="_______s______"></span><span id="_______S______"></span>**s**   
切换系统池与终端服务会话池之间的显示。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span>*TSSessionID*   
显示指定终端服务会话池中的分配。 *TSSessionID* 表示终端服务会话的会话 ID。 它必须是0到9之间的整数。 若要显示所有会话池或输入大于9的会话 Id，请使用 **i** 命令。

<span id="_______i______"></span><span id="_______I______"></span>**i**   
提示输入终端服务器会话的会话 ID。 可以通过以下两种方式进行响应：

-   若要显示所有终端服务会话池的分配，请按 ENTER。

-   若要显示特定终端服务会话池的分配，请键入会话 ID，然后按 ENTER。

<span id="_______l______"></span><span id="_______L______"></span>**l**   
切换打开和关闭已更改行的突出显示。

<span id="_______e______"></span><span id="_______E______"></span>**e**   
开启和关闭池总计。 总计显示在显示的底部。

<span id="_______t______"></span><span id="_______T______"></span>**t**   
按标记名排序。

<span id="_______a______"></span><span id="_______A______"></span>**一个**   
按分配数排序。 与圆括号字符一起使用时，键会按分配 **中的更改** 进行排序。

<span id="_______f______"></span><span id="_______F______"></span>**f**   
按免费操作数排序。 与括号字符一起使用时， **f** 键按自由操作的更改进行排序。

<span id="_______d______"></span><span id="_______D______"></span>**d**   
按分配的字节数和释放的字节数进行排序。

<span id="_______b______"></span><span id="_______B______"></span>**b**   
按使用的字节排序。 与圆括号字符一起使用时， **b** 键按使用的字节数进行排序。

<span id="_______m______"></span><span id="_______M______"></span>**m**   
按每个分配的字节数排序。 与圆括号字符一起使用时， **m** 键按分配的字节数进行排序。

<span id="_________or_h"></span><span id="_________OR_H"></span> **?** 或 **h**  
显示启动命令参数、运行时命令和 PoolMon 显示的说明。 若要关闭 "帮助" 显示，请按 ESC 键。

<span id="_______q_or_ESC"></span><span id="_______q_or_esc"></span><span id="_______Q_OR_ESC"></span>**q** 或 **ESC**  
停止 PoolMon。









