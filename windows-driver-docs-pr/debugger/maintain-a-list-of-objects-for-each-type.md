---
title: 维护每个类型的对象列表
description: 维护每个类型的对象列表
ms.assetid: 845ba6cb-60b3-4053-9d54-f43ed344f82d
keywords:
- 维护每个类型 （全局标志） 的对象的列表
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: b79010fbef678be9374226caa067e6258ddd223d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383310"
---
# <a name="maintain-a-list-of-objects-for-each-type"></a>维护每个类型的对象列表


## <span id="ddk_maintain_a_list_of_objects_for_each_type_dtools"></span><span id="DDK_MAINTAIN_A_LIST_OF_OBJECTS_FOR_EACH_TYPE_DTOOLS"></span>


**维护的每种类型的对象的列表**标志收集和维护的活动按对象类型，例如，事件、 mutex，和信号量对象的列表。

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
<td align="left"><p>整个系统的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

若要显示对象列表，请使用 sysinternals 工具[处理](https://docs.microsoft.com/sysinternals/downloads/handle)。

**请注意**  创建时设置此标志的链接的列表，为每个对象使用 8 个字节的开销。 请记住在分析完成后清除此标志。

 

 

 





