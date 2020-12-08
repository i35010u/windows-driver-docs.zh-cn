---
title: " (系统状态) "
description: 双竖线 ( ) 命令打印指定系统或当前正在调试的所有系统的状态。不要将此命令与 (处理状态) 命令混淆。
keywords:
- ) Windows 调试 (系统状态
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- (System Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd768b4b700ead1f2bad6bf18fe256d05343446f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800211"
---
# <a name="-system-status"></a>||（系统状态）


双竖线 (**||**) 命令打印指定系统或当前正在调试的所有系统的状态。

不要将此命令与 [**| (进程状态)**](---process-status-.md) 命令混淆。

```dbgcmd
|| System 
```

## <a name="span-idddk_cmd_system_status_dbgspanspan-idddk_cmd_system_status_dbgspanparameters"></a><span id="ddk_cmd_system_status_dbg"></span><span id="DDK_CMD_SYSTEM_STATUS_DBG"></span>参数


<span id="_______System______"></span><span id="_______system______"></span><span id="_______SYSTEM______"></span>*系统*   
指定要显示的系统。 如果省略此参数，则将显示正在调试的所有系统。 有关语法的详细信息，请参阅 [系统语法](system-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>多目标调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此 **||** 命令仅在调试多个目标时才有用。 许多（但不是全部）多目标调试会话涉及多个系统。 有关这些会话的详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

每个系统列表包括服务器名称和协议详细信息。 运行调试器的系统标识为 " **&lt; 本地 &gt;**"。

下面的示例演示如何使用此命令。 以下命令显示所有系统。

```dbgcmd
3:2:005> ||
```

以下命令还显示所有系统。

```dbgcmd
3:2:005> ||*
```

以下命令显示当前处于活动状态的系统。

```dbgcmd
3:2:005> ||.
```

以下命令显示具有最近的异常或中断的系统。

```dbgcmd
3:2:005> ||#
```

以下命令显示 "系统号 2"。

```dbgcmd
3:2:005> ||2
```

 

 





