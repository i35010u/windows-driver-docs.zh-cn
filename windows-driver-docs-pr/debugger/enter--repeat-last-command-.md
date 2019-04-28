---
title: ENTER（重复上一条命令）
description: ENTER 键重复刚才的最后一个命令。
ms.assetid: 058e455a-8934-4b28-8cf0-2d3f09a7e7cc
keywords:
- 输入 （重复执行最后一个命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ENTER (Repeat Last Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8bd72fad5a79c949b008ae271f5d89fe0d1e076f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347857"
---
# <a name="enter-repeat-last-command"></a>ENTER（重复上一条命令）


ENTER 键重复刚才的最后一个命令。

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 CDB 和 KD 中，按 ENTER 键本身在命令提示符下重新发出你之前输入的命令。

在 WinDbg 中，ENTER 键会产生任何效果，或可以使用它来重复前一命令。 此选项设置**选项**对话框。 (若要打开**选项**对话框中，单击**选项**上**视图**菜单或单击**选项**按钮 (![屏幕截图选项按钮的](images/tbopt.png)) 工具栏上。)

如果设置 ENTER 重复最后一个命令，但你想要创建中的空白[调试器命令窗口](debugger-command-window.md)，使用[  **\* （注释行说明符）** ](----comment-line-specifier-.md)令牌，然后按 ENTER 几次。

 

 





