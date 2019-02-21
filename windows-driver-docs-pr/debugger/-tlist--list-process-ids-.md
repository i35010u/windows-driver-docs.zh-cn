---
title: .tlist (列表进程 Id)
description: .Tlist 命令列出所有系统上运行的进程。
ms.assetid: 44d46b74-5cf1-4384-b468-baec5a87eaed
keywords:
- 列出进程 Id (.tlist) 命令
- 过程中，列表的进程 Id (.tlist) 命令
- .tlist (列表进程 Id) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .tlist (List Process IDs)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50a5182dcc140b561ae766d5b462a963e7360ab0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546697"
---
# <a name="tlist-list-process-ids"></a>.tlist (列表进程 Id)


**.Tlist**命令列出所有系统上运行的进程。

```dbgcmd
.tlist [Options][FileNamePattern]
```

## <a name="span-idddkmetalistprocessidsdbgspanspan-idddkmetalistprocessidsdbgspanparameters"></a><span id="ddk_meta_list_process_ids_dbg"></span><span id="DDK_META_LIST_PROCESS_IDS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是任意数量的以下选项：

<span id="-v"></span><span id="-V"></span>**-v**  
将导致显示详细信息。 这包括会话数、 过程用户名和命令行用于启动进程。

<span id="-c"></span><span id="-C"></span>**-c**  
将显示限制为仅在当前进程。

<span id="_______FileNamePattern______"></span><span id="_______filenamepattern______"></span><span id="_______FILENAMEPATTERN______"></span> *FileNamePattern*   
指定要显示的文件名称或进程的文件名称必须与匹配的模式。 将显示文件名称匹配此模式的进程。 *FileNamePattern*可能包含多个通配符和说明符; 请参阅[字符串通配符语法](string-wildcard-syntax.md)有关详细信息。 仅针对实际的文件名，不是路径执行此匹配项。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

显示进程的其他方法，请参阅[查找进程 ID](finding-the-process-id.md)。

<a name="remarks"></a>备注
-------

每个进程 ID 将显示**0n**前缀，以强调 PID 是一个十进制数。

 

 





