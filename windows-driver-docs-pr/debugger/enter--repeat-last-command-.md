---
title: ENTER（重复上一条命令）
description: ENTER 键重复您键入的最后一个命令。
keywords:
- 输入 (重复最后一个命令) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ENTER (Repeat Last Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 650e378adbe1f723853fa4dbb46207cf384a72eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820897"
---
# <a name="enter-repeat-last-command"></a>ENTER（重复上一条命令）


ENTER 键重复您键入的最后一个命令。

```dbgcmd
ENTER
```

## <span id="ddk_cmd_repeat_last_command_dbg"></span><span id="DDK_CMD_REPEAT_LAST_COMMAND_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
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

在 CDB 和 KD 中，在命令提示符下按 ENTER 键本身，重新发送之前输入的命令。

在 WinDbg 中，ENTER 键不起作用，或者您可以使用它来重复上一个命令。 您可以在 " **选项** " 对话框中设置此选项。  (打开 "**选项**" 对话框，单击 "**视图**" 菜单上的 "**选项**"，或单击工具栏上 "选项" 按钮)  (屏幕截图的 **"选项" 按钮** ![ ](images/tbopt.png) 。 ) 

如果设置 ENTER 以重复最后一个命令，但要在 [调试器命令窗口](debugger-command-window.md)中创建空格，请使用 [**\* (注释行说明符)**](----comment-line-specifier-.md)标记，然后按 enter 多次。

 

 





