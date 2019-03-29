---
title: Hostfont 注册表项
description: Hostfont 注册表项
ms.assetid: f7ce2591-197a-4094-8b21-5e0cc48506ea
keywords:
- 打印的 postScript 打印机驱动程序 WDK HostFontXxx 注册表项
- Pscript WDK 打印，HostFontXxx 注册表项
- HostFontXxx 注册表项 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3724e5fcd49ebd48875b94253914f7bc08c2d163
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464067"
---
# <a name="hostfont-registry-entries"></a>Hostfont 注册表项





插件的 OEM 可以通知 Pscript5 驱动程序 %hostfont%就绪 PostScript 解释器，有一组的字体和 CIDFonts 可供使用，它们是与 Pscript5 驱动程序可能在打印作业的过程中下载的相同。 通知字体的要处理这种方式是通过将密钥放在注册表中。 Pscript5 驱动程序将查看新的信息的注册表时其[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)调用函数。 该插件可以然后，确保数据是最新，然后才能启用 PDEV。

下表列出了 %hostfont%注册表条目名称、 其类型和它们的值。 插件 OEM 应调用 SetPrinterData （Microsoft Windows SDK 文档中所述） 来设置这些项的名称。 HostFont*Xxx*条目名称是互相排斥。 也就是说，只有一个下列条目名称可以注册表中存在在任何给定时间。

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
<p>可以包含多个，其中包含 PostScript CIDFont 名称的以 NULL 结尾的 ASCII 字符串。 最终的字符串由一个额外的 null 字符终止。</p></td>
<td><p>类似 HostFontExceptFonts，只不过它将应用于 CIDFonts。</p></td>
</tr>
<tr class="even">
<td><p>HostFontExceptFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个，其中包含 PostScript 字体名称的以 NULL 结尾的 ASCII 字符串。 最终的字符串由一个额外的 null 字符终止。</p></td>
<td><p>Pscript5 驱动程序看不到""作为可用，并且两者 %hostfont%就绪 PostScript 解释器中的这些字体的字体。 Pscript5 驱动程序下载仅这些字体。</p></td>
</tr>
<tr class="odd">
<td><p>HostFontHasMostFonts</p></td>
<td><p>REG_DWORD</p>
<p>可以是任何值。</p></td>
<td><p>将所有字体视为 %hostfont%-可以。 如果此条目名称将显示包含的任何值，Pscript5 驱动程序不会下载任何字体。</p></td>
</tr>
<tr class="even">
<td><p>HostFontIncludesCIDFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个，其中包含 PostScript CIDFont 名称的以 NULL 结尾的 ASCII 字符串。 最终的字符串由一个额外的 null 字符终止。</p></td>
<td><p>类似 HostFontIncludesFonts，只不过它将应用于 CIDFonts。</p></td>
</tr>
<tr class="odd">
<td><p>HostFontIncludesFonts</p></td>
<td><p>REG_BINARY</p>
<p>可以包含多个，其中包含 PostScript 字体名称的以 NULL 结尾的 ASCII 字符串。 最终的字符串由一个额外的 null 字符终止。</p></td>
<td><p>Pscript5 驱动程序"看到"与唯一的可用且 %hostfont%就绪 PostScript 解释器在完全相同的字体。 Pscript5 驱动程序不会下载这些字体。</p></td>
</tr>
</tbody>
</table>

 

### <a name="additional-notes-on-hostfont-registry-entry-names"></a>有关 Hostfont 注册表条目名称的其他说明

HostFontExceptFonts 是 REG\_包含的序列包含基于 TTF 基于 OTF 或基于 PFB 的编码的标志符号的名称-基于和字体的 PostScript findfont 名称以 NULL 结尾的单字节字符串的二进制数据。 名称列出顺序不分先后;由两个 null 值终止的最后一个名称和 null 值后有任何字节。 仅当找不到 HostFontHasMostFonts 时检查此项名称。

具有分配给它的任何值的 HostFontHasMostFonts 键存在意味着该驱动程序应假定所有基于 TTF 的、 基于 OTF PFB 基于主机的字体的形式提供的"本机"格式，即 PostScript 字体或作为 CIDFont 格式目标解释器上适当。

HostFontIncludesFonts 具有类似于 HostFontExceptFonts，只不过它显式列出目标解释器上可用的 PostScript 字体名称。

 

 




