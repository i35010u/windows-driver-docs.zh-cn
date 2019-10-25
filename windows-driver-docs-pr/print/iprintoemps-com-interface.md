---
title: IPrintOemPS COM 接口
description: IPrintOemPS COM 接口
ms.assetid: 504db6ab-291e-4fba-995d-49a22a3a7c7f
keywords:
- IPrintOemPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a121186b6f53f905fae6592209baff2f6ae60f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844320"
---
# <a name="iprintoemps-com-interface"></a>IPrintOemPS COM 接口





`IPrintOemPS` COM 接口是 Pscript5 的[打印机图形 DLL](printer-graphics-dll.md)与呈现插件进行通信的方式。 `IPrintOemPS` 接口由每个呈现插件实现。

下表列出并描述了 `IPrintOemPS` 接口提供的所有方法。 呈现插件必须定义所有列出的方法。 如果不需要方法，它可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command" data-raw-source="[&lt;strong&gt;IPrintOemPS::Command&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command)"><strong>IPrintOemPS：：命令</strong></a></p></td>
<td><p>允许使用呈现插件将 Postscript 命令插入打印作业的数据流。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-devmode" data-raw-source="[&lt;strong&gt;IPrintOemPS::DevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-devmode)"><strong>IPrintOemPS：:D evMode</strong></a></p></td>
<td><p>对呈现插件的私有<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>DEVMODEW</strong></a>成员执行操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disabledriver)"><strong>IPrintOemPS：:D isableDriver</strong></a></p></td>
<td><p>释放由呈现插件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)"><strong>IPrintOemPS：： EnableDriver</strong></a>方法分配的资源。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev)"><strong>IPrintOemPS：:D isablePDEV</strong></a></p></td>
<td><p>允许呈现插件删除由其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)"><strong>IPrintOemPS：： EnablePDEV</strong></a>方法分配的私有 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)"><strong>IPrintOemPS::EnableDriver</strong></a></p></td>
<td><p>允许呈现插件挂钩某些图形 DDI 函数。 请注意，必须将此方法和<strong>IPrintOemPS：:D isabledriver</strong>视为成对的;如果实现了一个，则还必须实现另一个。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)"><strong>IPrintOemPS::EnablePDEV</strong></a></p></td>
<td><p>允许呈现插件创建其自己的 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemPS::GetInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo)"><strong>IPrintOemPS：： GetInfo</strong></a></p></td>
<td><p>（需要实现。）返回呈现插件标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemPS::PublishDriverInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-publishdriverinterface)"><strong>IPrintOemPS：:P ublishDriverInterface</strong></a></p></td>
<td><p>（需要实现。）提供指向 Pscript5 驱动程序的<a href="iprintoemdriverps-com-interface.md" data-raw-source="[IPrintOemDriverPS COM interface](iprintoemdriverps-com-interface.md)">IPRINTOEMDRIVERPS com 接口</a>、 <a href="iprintcoreps2-com-interface.md" data-raw-source="[IPrintCorePS2 COM interface](iprintcoreps2-com-interface.md)">IPrintCorePS2 Com 接口</a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps" data-raw-source="[IPrintCoreHelperPS interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)">IPrintCoreHelperPS 接口</a>的指针。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev" data-raw-source="[&lt;strong&gt;IPrintOemPS::ResetPDEV&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev)"><strong>IPrintOemPS::ResetPDEV</strong></a></p></td>
<td><p>允许呈现插件重置其 PDEV 结构。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




