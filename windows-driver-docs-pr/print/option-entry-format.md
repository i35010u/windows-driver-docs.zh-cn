---
title: 选项格式
description: 选项格式
keywords:
- 打印机选项 WDK Unidrv，输入格式
- 格式化 WDK 打印机选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4f910d1aa514ec3113a8870f230eb83f4fd6a01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807699"
---
# <a name="option-entry-format"></a>选项格式





若要在 GPD 文件中指定打印机选项项，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>选项</strong>： <em>OptionName</em> { <em>OptionAttributes</em> }</p></td>
</tr>
</tbody>
</table>

 

其中， *OptionName* 是预定义的 [标准选项](standard-options.md) 之一的名称或自定义的选项名称，而 *OptionAttributes* 是一组 [选项属性](option-attributes.md)。

有关 \* 与功能相关联的一组 **选项** 条目的示例，请参阅 [功能输入格式](feature-entry-format.md)。

如果重复选项规范（例如，通过 \* 为 **PaperSize** 功能的字母选项指定两个或更多 *_选项_*），则选项条目中的每个重复选项属性将 \* *_Option_* 覆盖前一个选项，并且 GPD 分析器仅保留最后一个选项。 另一方面，如果 GPD 分析器遇到 \* **PaperSize** (或任何其他) 功能的两个或更多功能项，则 \* 不会将之前指定的 *_选项_* 项添加到分析器的数据库。

您可以控制向用户显示选项的顺序。 请参阅 [指定功能和选项显示顺序](specifying-feature-and-option-display-order.md)。

 

 




