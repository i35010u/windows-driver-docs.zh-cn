---
title: 下载字体命令
description: 下载字体命令
ms.assetid: 5cf6b2bd-5378-4e90-8959-ced978dee02f
keywords:
- 下载的字体命令 WDK Unidrv
- 字体的命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02ef483447c5f1a802b09867f46930ae4d332c76
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349398"
---
# <a name="commands-for-downloaded-fonts"></a>下载字体命令





下表列出了用于控制下载的字体的命令。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Command</th>
<th>描述</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdDeleteFont</strong></p></td>
<td><p>若要通过指定其标识符删除软字体的命令。</p></td>
<td><p>可选。 此命令仅当指定可以立即回收已删除的字体的已分配的内存。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdDeselectFontID</strong></p></td>
<td><p>若要取消当前的字体 ID 选择以使字体处于非活动状态的命令。</p></td>
<td><p>可选。 如果不存在，则不需要选择新字体时取消选择当前字体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectFontHeight</strong></p></td>
<td><p>若要选择已下载的字体的高度的命令。</p></td>
<td><p>可选。 如果不存在，则打印机不支持可缩放的、 可下载的 True Type 轮廓字体。 此命令需要 HPPCL_OUTLINE 格式。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectFontID</strong></p></td>
<td><p>要选择的当前字体 ID 以使字体处于活动状态的命令。</p></td>
<td><p>所需打印机是否支持下载的字体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectFontWidth</strong></p></td>
<td><p>若要选择已下载的字体的粗细的命令。</p></td>
<td><p>可选。 如果不存在，请下载字体的宽度是按比例缩放窗体的高度。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetCharCode</strong></p></td>
<td><p>若要指定要下载或删除的下一个字符的字符代码的命令。</p></td>
<td><p>所需打印机是否支持下载的字体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetFontID</strong></p></td>
<td><p>命令以设置当前字体 id。</p></td>
<td><p>所需打印机是否支持下载的字体。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




