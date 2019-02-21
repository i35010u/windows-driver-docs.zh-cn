---
title: ad （删除别名）
description: Ad 命令从别名列表中删除别名。
ms.assetid: 8ff223b6-5cfb-4d87-b45f-ad9bd51faf7f
keywords:
- ad （删除别名） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ad (Delete Alias)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e22b13edd36c4d97ed2a932e8e646b54972781bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544374"
---
# <a name="ad-delete-alias"></a>ad （删除别名）


**Ad**命令从别名列表中删除别名。

```dbgcmd
ad [/q] Name 
ad * 
```

## <a name="span-idddkcmddeletealiasdbgspanspan-idddkcmddeletealiasdbgspanparameters"></a><span id="ddk_cmd_delete_alias_dbg"></span><span id="DDK_CMD_DELETE_ALIAS_DBG"></span>参数


<span id="________q______"></span><span id="________Q______"></span> **/q**   
指定安静模式。 此模式下会隐藏错误消息，如果别名，*名称*指定不存在。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
指定要删除的别名的名称。 如果指定一个星号 (\*)，将删除所有别名 (即使其名称是的别名"\*")。

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

有关如何使用别名的详细信息，请参阅[Using 别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

可以使用**ad**命令以删除任何用户命名的别名。 但您不能使用此命令删除的固定名称别名 ($u0 到 $u9)。

 

 





