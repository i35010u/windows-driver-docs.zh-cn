---
title: IPrintOemPS COM 接口
description: IPrintOemPS COM 接口
keywords:
- IPrintOemPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a63e82d496d869cd82daa9cf15639c348f01295
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796559"
---
# <a name="iprintoemps-com-interface"></a>IPrintOemPS COM 接口





`IPrintOemPS`COM 接口是 Pscript5 的[打印机图形 DLL](printer-graphics-dll.md)与呈现插件进行通信的方式。 `IPrintOemPS`接口由每个呈现插件实现。

下表列出并描述了接口提供的所有方法 `IPrintOemPS` 。 呈现插件必须定义所有列出的方法。 如果方法不是必需的，则可以只返回 E \_ NOTIMPL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command" data-raw-source="[&lt;strong&gt;IPrintOemPS::Command&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command)"><strong>IPrintOemPS：：命令</strong></a></p></td>
<td><p>允许使用呈现插件将 Postscript 命令插入打印作业的数据流。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-devmode" data-raw-source="[&lt;strong&gt;IPrintOemPS::DevMode&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-devmode)"><strong>IPrintOemPS：:D evMode</strong></a></p></td>
<td><p>对呈现插件的私有 <a href="/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a> 成员执行操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisableDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disabledriver)"><strong>IPrintOemPS：:D isableDriver</strong></a></p></td>
<td><p>释放由呈现插件的 <a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)"><strong>IPrintOemPS：： EnableDriver</strong></a> 方法分配的资源。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisablePDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev)"><strong>IPrintOemPS：:D isablePDEV</strong></a></p></td>
<td><p>允许呈现插件删除由其 <a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)"><strong>IPrintOemPS：： EnablePDEV</strong></a> 方法分配的私有 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)"><strong>IPrintOemPS::EnableDriver</strong></a></p></td>
<td><p>允许呈现插件挂钩某些图形 DDI 函数。 请注意，必须将此方法和 <strong>IPrintOemPS：:D isabledriver</strong> 视为成对的;如果实现了一个，则还必须实现另一个。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)"><strong>IPrintOemPS::EnablePDEV</strong></a></p></td>
<td><p>允许呈现插件创建其自己的 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemPS::GetInfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo)"><strong>IPrintOemPS：： GetInfo</strong></a></p></td>
<td><p>需要 (实现。 ) 返回呈现插件标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemPS::PublishDriverInterface&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-publishdriverinterface)"><strong>IPrintOemPS：:P ublishDriverInterface</strong></a></p></td>
<td><p>需要 (实现。 ) 提供指向 Pscript5 驱动程序的 <a href="iprintoemdriverps-com-interface.md" data-raw-source="[IPrintOemDriverPS COM interface](iprintoemdriverps-com-interface.md)">IPRINTOEMDRIVERPS com 接口</a>、 <a href="iprintcoreps2-com-interface.md" data-raw-source="[IPrintCorePS2 COM interface](iprintcoreps2-com-interface.md)">IPrintCorePS2 Com 接口</a>或 <a href="/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps" data-raw-source="[IPrintCoreHelperPS interface](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)">IPrintCoreHelperPS 接口</a>的指针。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::ResetPDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev)"><strong>IPrintOemPS::ResetPDEV</strong></a></p></td>
<td><p>允许呈现插件重置其 PDEV 结构。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

