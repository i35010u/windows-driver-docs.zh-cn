---
title: 维护每个类型的对象列表
description: 维护每个类型的对象列表
ms.assetid: 845ba6cb-60b3-4053-9d54-f43ed344f82d
keywords:
- '为每个类型 (全局标志维护对象列表) '
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2e337dc933232cd24220ddacda5bd18dde07a03d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217368"
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

**注意**   设置此标志时创建的链接列表对每个对象使用8个字节的系统开销。 请记得在分析完成后清除此标志。

 

 

