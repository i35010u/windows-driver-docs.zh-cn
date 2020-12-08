---
title: .tlist（列出进程 ID）
description: Tlist.exe 命令列出系统上运行的所有进程。
keywords:
- 列出进程 Id ( tlist.exe) 命令
- 进程，列出进程 Id ( tlist.exe) 命令
- tlist.exe (列出) Windows 调试的进程 Id
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .tlist (List Process IDs)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a78cc55a123d2a0d4db0baf0e4acc6f04e413499
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838837"
---
# <a name="tlist-list-process-ids"></a>.tlist（列出进程 ID）


**Tlist.exe** 命令列出系统上运行的所有进程。

```dbgcmd
.tlist [Options][FileNamePattern]
```

## <a name="span-idddk_meta_list_process_ids_dbgspanspan-idddk_meta_list_process_ids_dbgspanparameters"></a><span id="ddk_meta_list_process_ids_dbg"></span><span id="DDK_META_LIST_PROCESS_IDS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列任意数量的选项：

<span id="-v"></span><span id="-V"></span>**-v**  
使显示更详细。 这包括会话号码、进程用户名和用于启动进程的命令行。

<span id="-c"></span><span id="-C"></span>**-c**  
仅显示当前进程的显示范围。

<span id="_______FileNamePattern______"></span><span id="_______filenamepattern______"></span><span id="_______FILENAMEPATTERN______"></span>*FileNamePattern*   
指定要显示的文件名或进程的文件名必须匹配的模式。 仅显示文件名与此模式匹配的进程。 *FileNamePattern* 可能包含各种通配符和说明符;有关详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md) 。 此匹配仅针对实际的文件名，而不是路径。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关显示进程的其他方法，请参阅 [查找进程 ID](finding-the-process-id.md)。

<a name="remarks"></a>备注
-------

每个进程 ID 都显示有一个 **0n** 前缀，以强调 PID 是一个十进制数。

 

 





