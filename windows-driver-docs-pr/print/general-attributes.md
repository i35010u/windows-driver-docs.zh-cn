---
title: 常规属性
description: 常规属性
keywords:
- 打印机属性 WDK Unidrv，常规
- 常规打印机属性 WDK Unidrv
- 一般打印机属性 WDK Unidrv，关于常规打印机属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b7e504f2f31f288d15f8b8cf70b67af043206b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796909"
---
# <a name="general-attributes"></a>常规属性





*常规属性* 表示由 GPD 语言定义的 [属性类型](attribute-types.md) 之一。 常规属性不与特定功能或选项关联。 常规属性分为以下几组：

[仅限根级别的属性](root-level-only-attributes.md)

[常规打印属性](general-printing-attributes.md)

[文本打印属性](text-printing-attributes.md)

[光栅打印属性](raster-printing-attributes.md)

[矢量打印属性](vector-printing-attributes.md)

通常情况下，会在 GPD 文件中的根 (级别（而不是大括号) 内）放置所有常规属性。 根级别的属性必须始终置于根级别。

偶尔，常规属性的值 (除了仅限根级别的属性) ，它依赖于配置参数。 在这种情况下，属性项可能位于 \* option 语句内，或者位于[ \* case](conditional-statements.md)语句中 (位于根级别或包含在 \* option 语句) 中。 如果该属性不在根级别 (因为它包含在 \* 选项语句中或者在) nonroot 级 \* Case 语句中，所以属性名称必须以 EXTERN \_ GLOBAL 符号为前缀，如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>EXTERN_GLOBAL： *<em>AttributeName</em>： <em>AttributeValue</em></p></td>
</tr>
</tbody>
</table>

 

有关指定配置依赖项的详细信息，请参阅 [条件语句](conditional-statements.md)。

 

 




