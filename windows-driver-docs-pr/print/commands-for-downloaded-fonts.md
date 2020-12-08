---
title: 下载字体命令
description: 下载字体命令
keywords:
- 下载的字体命令 WDK Unidrv
- font 命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a046e0c599485fb63eac74d9fb31e3268392160
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797635"
---
# <a name="commands-for-downloaded-fonts"></a>下载字体命令





下表列出了用于控制已下载字体的命令。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令</th>
<th>描述</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdDeleteFont</strong></p></td>
<td><p>命令通过指定其标识符来删除软字体。</p></td>
<td><p>可选。 仅当可以立即回收已删除字体的分配内存时，才指定此命令。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdDeselectFontID</strong></p></td>
<td><p>用于取消选择当前字体 ID 以使字体处于非活动状态的命令。</p></td>
<td><p>可选。 如果不存在，则在选择新字体时不需要取消选择当前字体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectFontHeight</strong></p></td>
<td><p>用于选择已下载字体的高度的命令。</p></td>
<td><p>可选。 如果不存在，则打印机不支持可缩放的、可下载的 True 类型轮廓字体。 HPPCL_OUTLINE 格式需要此命令。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectFontID</strong></p></td>
<td><p>用于选择当前字体 ID 以使字体活动的命令。</p></td>
<td><p>如果打印机支持下载的字体，则为必需。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectFontWidth</strong></p></td>
<td><p>用于选择已下载字体宽度的命令。</p></td>
<td><p>可选。 如果不存在，则下载字体的宽度按比例比例缩放。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetCharCode</strong></p></td>
<td><p>用于指定要下载或删除的下一个字符的字符代码的命令。</p></td>
<td><p>如果打印机支持下载的字体，则为必需。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetFontID</strong></p></td>
<td><p>用于设置当前字体 ID 的命令。</p></td>
<td><p>如果打印机支持下载的字体，则为必需。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




