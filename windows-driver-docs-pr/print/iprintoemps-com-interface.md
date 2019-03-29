---
title: IPrintOemPS COM 接口
description: IPrintOemPS COM 接口
ms.assetid: 504db6ab-291e-4fba-995d-49a22a3a7c7f
keywords:
- IPrintOemPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936ccd8ddb014f8a8ad0f25c89b3bfc341da7c04
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349574"
---
# <a name="iprintoemps-com-interface"></a>IPrintOemPS COM 接口





`IPrintOemPS` COM 接口是方式的情况[打印机图形 DLL](printer-graphics-dll.md)为 Pscript5 呈现插件与进行通信。 `IPrintOemPS`接口由每个呈现插件实现。

下表列出并描述所有提供的方法`IPrintOemPS`接口。 呈现插件必须定义所有列出的方法。 如果不需要一种方法，则可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553199" data-raw-source="[&lt;strong&gt;IPrintOemPS::Command&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553199)"><strong>IPrintOemPS::Command</strong></a></p></td>
<td><p>允许呈现插件，以将 Postscript 命令插入到打印作业的数据的流。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553205" data-raw-source="[&lt;strong&gt;IPrintOemPS::DevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553205)"><strong>IPrintOemPS::DevMode</strong></a></p></td>
<td><p>执行操作上呈现插件的私有<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>成员。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553207" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553207)"><strong>IPrintOemPS::DisableDriver</strong></a></p></td>
<td><p>释放所分配的呈现插件的资源<a href="https://msdn.microsoft.com/library/windows/hardware/ff553212" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553212)"> <strong>IPrintOemPS::EnableDriver</strong> </a>方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553209" data-raw-source="[&lt;strong&gt;IPrintOemPS::DisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553209)"><strong>IPrintOemPS::DisablePDEV</strong></a></p></td>
<td><p>允许呈现插件，以删除由分配的专用 PDEV 结构及其<a href="https://msdn.microsoft.com/library/windows/hardware/ff553215" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553215)"> <strong>IPrintOemPS::EnablePDEV</strong> </a>方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553212" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553212)"><strong>IPrintOemPS::EnableDriver</strong></a></p></td>
<td><p>允许呈现插件出一些图形 DDI 函数挂钩。 请注意，此方法和<strong>IPrintOemPS::DisableDriver</strong>必须考虑作为对; 如果实现了一个，也必须实现其他。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553215" data-raw-source="[&lt;strong&gt;IPrintOemPS::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553215)"><strong>IPrintOemPS::EnablePDEV</strong></a></p></td>
<td><p>允许呈现插件，以创建其自己 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553221" data-raw-source="[&lt;strong&gt;IPrintOemPS::GetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553221)"><strong>IPrintOemPS::GetInfo</strong></a></p></td>
<td><p>（所需的实现。）返回呈现插件标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553228" data-raw-source="[&lt;strong&gt;IPrintOemPS::PublishDriverInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553228)"><strong>IPrintOemPS::PublishDriverInterface</strong></a></p></td>
<td><p>（所需的实现。）提供一个指向 Pscript5 驱动<a href="iprintoemdriverps-com-interface.md" data-raw-source="[IPrintOemDriverPS COM interface](iprintoemdriverps-com-interface.md)">IPrintOemDriverPS COM 接口</a>， <a href="iprintcoreps2-com-interface.md" data-raw-source="[IPrintCorePS2 COM interface](iprintcoreps2-com-interface.md)">IPrintCorePS2 COM 接口</a>，或<a href="https://msdn.microsoft.com/library/windows/hardware/ff552906" data-raw-source="[IPrintCoreHelperPS interface](https://msdn.microsoft.com/library/windows/hardware/ff552906)">IPrintCoreHelperPS 接口</a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553233" data-raw-source="[&lt;strong&gt;IPrintOemPS::ResetPDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553233)"><strong>IPrintOemPS::ResetPDEV</strong></a></p></td>
<td><p>允许呈现插件，以重置其 PDEV 结构。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




