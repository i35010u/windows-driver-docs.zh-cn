---
title: 选项格式
description: 选项格式
ms.assetid: defc035a-d571-4bf1-abeb-c7528ba23b81
keywords:
- 打印机选项 WDK Unidrv，条目格式
- 格式 WDK 打印机选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 687d7ccbd26df18f635f99a42ff1e40e0c804507
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366560"
---
# <a name="option-entry-format"></a>选项格式





若要在 GPD 文件中指定打印机选项条目，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>选项</strong>:<em>OptionName</em> { <em>OptionAttributes</em> }</p></td>
</tr>
</tbody>
</table>

 

其中*OptionName*是一个预定义的名称[标准选项](standard-options.md)或自定义的选项名称，并*OptionAttributes*是一套[选项属性](option-attributes.md)。

有关示例的一套\***选项**条目相关联的功能，请参阅[功能条目格式](feature-entry-format.md)。

如果您要重复的选项规范，例如通过指定两个或多个\***选项**条目**PaperSize**功能的盘符选项，在每个重复的选项属性\***选项**条目将覆盖上一个和 GPD 分析器只保留遇到的最后一个。 另一方面，如果 GPD 分析程序遇到两个或多个\*功能的条目**PaperSize** （或任何其他） 功能， \***选项**之前未指定的项添加到分析器的数据库。

您可以控制向用户显示选项的顺序。 请参阅[指定的功能和选项显示顺序](specifying-feature-and-option-display-order.md)。

 

 




