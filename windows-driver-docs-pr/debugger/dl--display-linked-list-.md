---
title: dl（显示链接的列表）
description: Dl 命令显示 LIST_ENTRY 或 SINGLE_LIST_ENTRY 链接的列表。
keywords:
- dl (显示) Windows 调试的链接列表
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dl (Display Linked List)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b7efb02be05c041bed429152ab5453def8ac33ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836551"
---
# <a name="dl-display-linked-list"></a>dl（显示链接的列表）


**Dl** 命令显示列表 \_ 项或单个 \_ 列表 \_ 项链接列表。

```dbgcmd
dl[b] Address MaxCount Size
```

## <a name="span-idddk_cmd_display_linked_list_dbgspanspan-idddk_cmd_display_linked_list_dbgspanparameters"></a><span id="ddk_cmd_display_linked_list_dbg"></span><span id="DDK_CMD_DISPLAY_LINKED_LIST_DBG"></span>参数


<span id="_______b______"></span><span id="_______B______"></span>**b**   
如果包括此项，则按逆序转储列表。  (换言之，调试器会跟随 **闪烁** s 而不是 **Flink**。 ) 此项不能用于单个 \_ 列表 \_ 项。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
列表的起始地址。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。

<span id="_______MaxCount______"></span><span id="_______maxcount______"></span><span id="_______MAXCOUNT______"></span>*MaxCount*   
要转储的元素的最大数目。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
每个元素的大小。 这是 \_ 将针对列表中的每个元素显示的连续 ULONG PTRs 的数目。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

此列表必须是列表 \_ 项或单个 \_ 列表 \_ 条目结构。 如果此项嵌入在较大的结构中，请确保该 *地址* 指向链接的列表结构，而不是指向外部结构的开头。

显示以 *Address* 开头。 因此，如果要提供指向列表开头的指针地址，则应忽略打印的第一个元素。

" *Address*"、" *MaxCount*" 和 " *Size* " 参数位于当前默认基数。 可以使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令或 **0x** 前缀来更改基数。

如果列表自行循环，则转储将停止。 如果遇到空指针，则转储将停止。

如果要对列表中的每个元素执行某个命令，请使用 [**！ list**](-list.md) 扩展。

 

 





