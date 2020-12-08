---
title: 维护每个类型的对象列表
description: 维护每个类型的对象列表
keywords:
- '为每个类型 (全局标志维护对象列表) '
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13842b6494c8938ec54381676553688229328142
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838813"
---
# <a name="maintain-a-list-of-objects-for-each-type"></a>维护每个类型的对象列表


## <span id="ddk_maintain_a_list_of_objects_for_each_type_dtools"></span><span id="DDK_MAINTAIN_A_LIST_OF_OBJECTS_FOR_EACH_TYPE_DTOOLS"></span>


**维护每个类型标志的对象列表**，按对象类型（例如，事件、mutex 和信号量）收集并维护活动对象的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>otl</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x4000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_MAINTAIN_OBJECT_TYPELIST</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

若要显示对象列表，请使用 sysinternals 工具 [句柄](/sysinternals/downloads/handle)。

**注意**   设置此标志时创建的链接列表对每个对象使用8个字节的系统开销。 请记得在分析完成后清除此标志。

 

 

