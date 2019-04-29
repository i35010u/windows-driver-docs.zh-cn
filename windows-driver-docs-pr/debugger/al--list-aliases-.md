---
title: al（列出别名）
description: Al 命令显示所有当前定义的用户命名别名的列表。
ms.assetid: 40e20edb-4545-4c5a-bb56-61e00b064efc
keywords:
- al （列表别名） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- al (List Aliases)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7cac3302ab00f1c88cbf4a3e35d054b942ec36b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355005"
---
# <a name="al-list-aliases"></a>al（列出别名）


**Al**命令显示所有当前定义的用户命名别名的列表。

```dbgcmd
al
```

## <span id="ddk_cmd_list_aliases_dbg"></span><span id="DDK_CMD_LIST_ALIASES_DBG"></span>


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

**Al**命令将列出所有用户命名的别名。 但是，此命令不会列出固定名称的别名 ($u0 到 $u9)。

 

 





