---
title: dl（显示链接的列表）
description: Dl 命令显示 LIST_ENTRY 或 SINGLE_LIST_ENTRY 链接的列表。
ms.assetid: fbf03e78-d4b3-4dd9-904b-3f44a1a86cff
keywords:
- dl （显示链接列表） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dl (Display Linked List)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9998c5567a4e5ce43cc069e84487b065541450e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363919"
---
# <a name="dl-display-linked-list"></a>dl（显示链接的列表）


**Dl**命令显示列表\_条目或 SINGLE\_列表\_条目链接的列表。

```dbgcmd
dl[b] Address MaxCount Size
```

## <a name="span-idddkcmddisplaylinkedlistdbgspanspan-idddkcmddisplaylinkedlistdbgspanparameters"></a><span id="ddk_cmd_display_linked_list_dbg"></span><span id="DDK_CMD_DISPLAY_LINKED_LIST_DBG"></span>参数


<span id="_______b______"></span><span id="_______B______"></span> **b**   
如果包含，列表将按相反的顺序转储。 (换句话说，调试器遵循**闪烁**而不是 s **Flink**s。)这不能用于将单个\_列表\_条目。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
列表的起始地址。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______MaxCount______"></span><span id="_______maxcount______"></span><span id="_______MAXCOUNT______"></span> *MaxCount*   
要转储的元素的最大数目。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
每个元素的大小。 这是连续的 ULONG 的数\_将显示在列表中每个元素的合作伙伴。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

此列表必须是列表\_条目或 SINGLE\_列表\_条目结构。 如果这嵌入在更大的结构，请确保*地址*指向链接的列表结构而不指向外部结构的开头。

显示开头*地址*。 因此，如果你所提供的指向列表的开头的指针的地址，你应忽略打印的第一个元素。

*地址*， *MaxCount*，并*大小*参数位于当前的默认基数。 可以使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令或**0x**前缀来更改基数。

如果列表循环对自身，将停止转储。 如果遇到 null 指针，则将停止转储。

如果你想要执行的每个元素的列表的一些命令，使用[ **！ 列表**](-list.md)扩展。

 

 





