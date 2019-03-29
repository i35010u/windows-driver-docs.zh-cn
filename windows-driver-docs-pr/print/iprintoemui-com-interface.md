---
title: IPrintOemUI COM 接口
description: IPrintOemUI COM 接口
ms.assetid: 7fd4071a-11ce-49e6-9e23-4f0643da1d98
keywords:
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a36cdab836d208cf90c5cd6aa458f066d4441f0
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350422"
---
# <a name="iprintoemui-com-interface"></a>IPrintOemUI COM 接口





`IPrintOemUI` COM 接口是方式的情况[打印机接口 DLL](printer-interface-dll.md)为 Unidrv 或 Pscript5 插件的 UI 与通信。 `IPrintOemUI`接口实现的每个插件的 UI。

下表列出并描述所有方法的`IPrintOemUI`接口提供。 UI 插件必须定义所有列出的方法。 如果不需要一种方法，则可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554159" data-raw-source="[&lt;strong&gt;IPrintOemUI::CommonUIProp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554159)"><strong>IPrintOemUI::CommonUIProp</strong></a></p></td>
<td><p>允许插件的 UI 来修改现有打印机属性表页或文档属性表页。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554162" data-raw-source="[&lt;strong&gt;IPrintOemUI::DeviceCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554162)"><strong>IPrintOemUI::DeviceCapabilities</strong></a></p></td>
<td><p>允许插件 UI 以指定自定义的设备功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554165" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevicePropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554165)"><strong>IPrintOemUI::DevicePropertySheets</strong></a></p></td>
<td><p>允许 UI 插件以向打印机设备的打印机属性表添加新页面。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554167" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554167)"><strong>IPrintOemUI::DevMode</strong></a></p></td>
<td><p>执行操作 UI 插件的私有<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>成员。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554172" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevQueryPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554172)"><strong>IPrintOemUI::DevQueryPrintEx</strong></a></p></td>
<td><p>允许插件的 UI 来帮助确定是否可打印打印作业。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554173" data-raw-source="[&lt;strong&gt;IPrintOemUI::DocumentPropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554173)"><strong>IPrintOemUI::DocumentPropertySheets</strong></a></p></td>
<td><p>允许 UI 插件以向打印机设备的文档属性表添加新页面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554175" data-raw-source="[&lt;strong&gt;IPrintOemUI::DriverEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554175)"><strong>IPrintOemUI::DriverEvent</strong></a></p></td>
<td><p>当处理可能需要采取措施通过打印机驱动程序的驱动程序特定事件时，由打印后台处理程序调用。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554176" data-raw-source="[&lt;strong&gt;IPrintOemUI::FontInstallerDlgProc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554176)"><strong>IPrintOemUI::FontInstallerDlgProc</strong></a></p></td>
<td><p>将替换 Unidrv 字体安装程序的用户界面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554178" data-raw-source="[&lt;strong&gt;IPrintOemUI::GetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554178)"><strong>IPrintOemUI::GetInfo</strong></a></p></td>
<td><p>（所需的实现。）返回 UI 插件的标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554182" data-raw-source="[&lt;strong&gt;IPrintOemUI::PrinterEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554182)"><strong>IPrintOemUI::PrinterEvent</strong></a></p></td>
<td><p>允许 UI 插件处理打印机事件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554184" data-raw-source="[&lt;strong&gt;IPrintOemUI::PublishDriverInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554184)"><strong>IPrintOemUI::PublishDriverInterface</strong></a></p></td>
<td><p>（所需的实现。）提供一个指向 Unidrv 或 Pscript5 驱动程序<a href="iprintoemdriverui-com-interface.md" data-raw-source="[IPrintOemDriverUI COM interface](iprintoemdriverui-com-interface.md)">IPrintOemDriverUI COM 接口</a>， <a href="iprintcoreui2-com-interface.md" data-raw-source="[IPrintCoreUI2 COM interface](iprintcoreui2-com-interface.md)">IPrintCoreUI2 COM 接口</a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff552906" data-raw-source="[IPrintCoreHelperPS interface](https://msdn.microsoft.com/library/windows/hardware/ff552906)">IPrintCoreHelperPS 接口</a>，或者<a href="https://msdn.microsoft.com/library/windows/hardware/ff552940" data-raw-source="[IPrintCoreHelperUni interface](https://msdn.microsoft.com/library/windows/hardware/ff552940)">IPrintCoreHelperUni 接口</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554186" data-raw-source="[&lt;strong&gt;IPrintOemUI::QueryColorProfile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554186)"><strong>IPrintOemUI::QueryColorProfile</strong></a></p></td>
<td><p>使打印机接口 DLL 以指定颜色管理 ICC 配置文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554188" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpdateExternalFonts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554188)"><strong>IPrintOemUI::UpdateExternalFonts</strong></a></p></td>
<td><p>启用 DLL 要更新的打印机的打印机接口<a href="customized-font-management.md#ddk-unidrv-font-format-files-gg" data-raw-source="[Unidrv font format files](customized-font-management.md#ddk-unidrv-font-format-files-gg)">Unidrv 字体格式文件</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554189" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpgradePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554189)"><strong>IPrintOemUI::UpgradePrinter</strong></a></p></td>
<td><p>允许插件的 UI 来升级设备注册表中存储的选项值。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




