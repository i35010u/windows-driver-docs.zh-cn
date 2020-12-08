---
title: ad（删除别名）
description: Ad 命令从别名列表中删除别名。
keywords:
- ad () Windows 调试中删除别名
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ad (Delete Alias)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 969d18d4cd140a94f0f705257d3038c6b8c7be7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799827"
---
# <a name="ad-delete-alias"></a>ad（删除别名）


**Ad** 命令从别名列表中删除别名。

```dbgcmd
ad [/q] Name 
ad * 
```

## <a name="span-idddk_cmd_delete_alias_dbgspanspan-idddk_cmd_delete_alias_dbgspanparameters"></a><span id="ddk_cmd_delete_alias_dbg"></span><span id="DDK_CMD_DELETE_ALIAS_DBG"></span>参数


<span id="________q______"></span><span id="________Q______"></span>**/q**   
指定安静模式。 如果 *名称* 指定的别名不存在，此模式将隐藏错误消息。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
指定要删除的别名的名称。 如果指定星号 (\*) ，则即使存在名称为 "" ) 的别名， (也将删除所有别名 \* 。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用别名的详细信息，请参阅 [使用别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

可以使用 **ad** 命令删除任何用户命名的别名。 但不能使用此命令删除固定名称别名 ($u 0 $u 9) 。

 

 





