---
title: ls、lsa（列出源行）
description: Ls 和 lsa 命令显示来自当前源文件的一系列行，并提升当前的源行号。
keywords:
- ls，lsa (列出 Windows 调试) 源行
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ls, lsa (List Source Lines)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9aef3c472ad7fc0fd11d153395ee57709109ea1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783467"
---
# <a name="ls-lsa-list-source-lines"></a>ls、lsa（列出源行）


**Ls** 和 **lsa** 命令显示来自当前源文件的一系列行，并提升当前的源行号。

```dbgcmd
ls [.] [first] [, count] 
lsa [.] address [, first [, count]] 
```

## <a name="span-idddk_cmd_list_source_lines_dbgspanspan-idddk_cmd_list_source_lines_dbgspanparameters"></a><span id="ddk_cmd_list_source_lines_dbg"></span><span id="DDK_CMD_LIST_SOURCE_LINES_DBG"></span>参数


 **.**   
使命令查找调试器引擎或 [**srcpath (设置源路径)**](-srcpath---lsrcpath--set-source-path-.md) 命令所使用的源文件。 如果未包含时间 **段 ()** ， **ls** 将使用最近加载的文件，并将 [**lsf (Load Source file)**](lsf--lsf---load-or-unload-source-file-.md) 命令一起使用。

<span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定从其开始源显示的地址。

有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______first______"></span><span id="_______FIRST______"></span>*第一个*   
指定要显示的第一行。 默认值为当前行。

<span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
指定要显示的行数。 默认值为 20 (0x14) ，除非已使用 [**lsp-a**](lsp--set-number-of-source-lines-.md) 命令更改了默认值。

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

运行 **ls** 或 **lsa** 命令后，当前行将重新定义为显示的最后一行。 当前行用于未来的 **ls**、 **lsa** 和 [**lsc**](lsc--list-current-source-.md) 命令。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**lsc（列出当前源）**](lsc--list-current-source-.md)

[**lsf、lsf-（加载或卸载源文件）**](lsf--lsf---load-or-unload-source-file-.md)

 

 






