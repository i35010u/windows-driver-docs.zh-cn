---
title: Hostfont 注册表项
description: Hostfont 注册表项
keywords:
- PostScript 打印机驱动程序 WDK 打印，HostFontXxx 注册表项
- Pscript WDK 打印，HostFontXxx 注册表项
- HostFontXxx 注册表项 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242cf27c401c090dc31d969ee25374e397c09521
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796855"
---
# <a name="hostfont-registry-entries"></a>Hostfont 注册表项





OEM 插件可以通知 Pscript5 驱动程序% hostfont% ready PostScript 解释器具有一组可供使用的字体和 CIDFonts，它们与 Pscript5 驱动程序可能会在打印作业中下载的字体和相同。 通过在注册表中放置密钥来以这种方式处理哪些字体。 当调用 Pscript5 驱动程序的 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数时，该驱动程序将检查注册表中是否有新的信息。 在启用 PDEV 之前，该插件可以确保数据是最新的。

下表列出了% hostfont% 注册表项名称、它们的类型及其值。 OEM 插件应调用 Microsoft Windows SDK 文档) 中所述的 SetPrinterData (，以设置这些项名称。 HostFont *Xxx* 条目名称互斥。 也就是说，在任何给定时间，注册表中只能存在以下条目名称之一。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表项名称</th>
<th>类型和值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HostFontExceptCIDFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个以 NULL 结尾的 ASCII 字符串，其中包含 PostScript CIDFont 名称。 最终字符串由一个额外的 null 字符终止。</p></td>
<td><p>类似于 HostFontExceptFonts，只不过它适用于 CIDFonts。</p></td>
</tr>
<tr class="even">
<td><p>HostFontExceptFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个以 NULL 结尾的 ASCII 字符串，其中包含 PostScript 字体名称。 最终字符串由一个额外的 null 字符终止。</p></td>
<td><p>Pscript5 驱动程序未 "查看" 的字体，并且与% hostfont%-ready PostScript 解释器中的字体完全相同。 Pscript5 驱动程序仅下载这些字体。</p></td>
</tr>
<tr class="odd">
<td><p>HostFontHasMostFonts</p></td>
<td><p>REG_DWORD</p>
<p>可以是任何值。</p></td>
<td><p>将所有字体视为% hostfont%。 如果此项名称与任何值一起显示，则 Pscript5 驱动程序不会下载任何字体。</p></td>
</tr>
<tr class="even">
<td><p>HostFontIncludesCIDFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个以 NULL 结尾的 ASCII 字符串，其中包含 PostScript CIDFont 名称。 最终字符串由一个额外的 null 字符终止。</p></td>
<td><p>类似于 HostFontIncludesFonts，只不过它适用于 CIDFonts。</p></td>
</tr>
<tr class="odd">
<td><p>HostFontIncludesFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个以 NULL 结尾的 ASCII 字符串，其中包含 PostScript 字体名称。 最终字符串由一个额外的 null 字符终止。</p></td>
<td><p>Pscript5 驱动程序 "看到" 唯一可用且在% hostfont%-ready PostScript 解释器中相同的字体。 Pscript5 驱动程序不会下载这些字体。</p></td>
</tr>
</tbody>
</table>

 

### <a name="additional-notes-on-hostfont-registry-entry-names"></a>有关 Hostfont 注册表项名称的其他说明

HostFontExceptFonts 是 \_ 包含以 NULL 结尾的单字节字符串序列的 REG 二进制数据，其中包含基于 .ttf、OTF 或 PFB 的基于编码和字形的字体的 PostScript findfont 名称。 名称以无特定顺序列出;姓氏以两个 Null 值终止，空值之后没有字节。 仅当找不到 HostFontHasMostFonts 时，才会检查此项名称。

如果存在具有分配给它的任何值的 HostFontHasMostFonts 键，则表明驱动程序应假定所有基于 .TTF、OTF 和 PFB 的主机字体都在目标解释器上以其 "本机" 格式提供，即，作为 PostScript 字体或 CIDFont 格式提供。

HostFontIncludesFonts 类似于 HostFontExceptFonts，只不过它显式列出了目标解释器上可用的 PostScript 字体名称。

 

