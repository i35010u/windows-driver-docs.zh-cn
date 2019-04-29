---
title: ls、lsa（列出源行）
description: Ls 和 lsa 命令显示一系列的当前源文件中的行，促进当前的源行号。
ms.assetid: ca5cd2f7-4920-4d36-b338-c934451bc511
keywords:
- ls、 lsa （列表源行） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ls, lsa (List Source Lines)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ff14372ab89b3458bacd43e782d87b23132d5cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383323"
---
# <a name="ls-lsa-list-source-lines"></a>ls、lsa（列出源行）


**Ls**并**lsa**命令显示一系列的当前源文件中的行和提升当前的源行号。

```dbgcmd
ls [.] [first] [, count] 
lsa [.] address [, first [, count]] 
```

## <a name="span-idddkcmdlistsourcelinesdbgspanspan-idddkcmdlistsourcelinesdbgspanparameters"></a><span id="ddk_cmd_list_source_lines_dbg"></span><span id="DDK_CMD_LIST_SOURCE_LINES_DBG"></span>参数


 **.**   
使调试器引擎的命令以查找源文件或[ **.srcpath （设置源路径）** ](-srcpath---lsrcpath--set-source-path-.md)使用的命令。 如果句点 (**。**) 不包括**ls**使用的文件的最近一次加载了[ **lsf （负载源文件）** ](lsf--lsf---load-or-unload-source-file-.md)命令。

<span id="_______address______"></span><span id="_______ADDRESS______"></span> *address*   
指定源显示即将开始的地址。

有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______first______"></span><span id="_______FIRST______"></span> *first*   
指定要显示的第一个行。 默认值为当前行。

<span id="_______count______"></span><span id="_______COUNT______"></span> *count*   
指定要显示的行的数量。 默认值为 20 (0x14)，除非已使用更改默认值[ **lsp-a** ](lsp--set-number-of-source-lines-.md)命令。

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

运行后**ls**或**lsa**命令时，当前行重新定义为显示加一的最后一行。 在将来使用的当前行**ls**， **lsa**，并[ **lsc** ](lsc--list-current-source-.md)命令。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**lsc （列表当前源）**](lsc--list-current-source-.md)

[**lsf，lsf-（加载或卸载源文件）**](lsf--lsf---load-or-unload-source-file-.md)

 

 






