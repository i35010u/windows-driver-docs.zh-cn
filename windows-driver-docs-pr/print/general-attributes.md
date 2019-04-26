---
title: 常规属性
description: 常规属性
ms.assetid: c48fabff-0580-478f-b423-d959815bbeb4
keywords:
- 打印机属性 WDK Unidrv，常规
- 常规打印机属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv 有关常规打印机属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e2afe6c70846e5b0fc39cf551e277832391d7a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329831"
---
# <a name="general-attributes"></a>常规属性





*常规属性*表示之一[属性类型](attribute-types.md)GPD 语言定义的。 常规属性不与特定的功能或选项相关联。 常规属性分为以下组：

[仅在根级别的属性](root-level-only-attributes.md)

[常规打印特性](general-printing-attributes.md)

[文本打印属性](text-printing-attributes.md)

[光栅打印属性](raster-printing-attributes.md)

[向量打印属性](vector-printing-attributes.md)

通常情况下，将所有的常规属性放在根级别 GPD 文件 (即，而不是在大括号)。 始终必须在根级别放置仅在根级别的属性。

有时，常规属性 （除外的仅限根级别的属性） 的值是依赖于配置参数。 在这种情况下，属性条目可能会放在\*Option 语句，或在[\*用例](conditional-statements.md)语句 (位于在根级别或包含在\*选项语句)。 如果该属性不是在根级别 (因为它包含在\*Option 语句或处于非根级别\*Case 语句)，属性名称必须以前缀 EXTERN\_全局符号，按如下所示:

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>EXTERN_GLOBAL: *<em>AttributeName</em>:<em>AttributeValue</em></p></td>
</tr>
</tbody>
</table>

 

有关指定配置依赖关系的详细信息，请参阅[条件语句](conditional-statements.md)。

 

 




