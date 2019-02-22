---
title: IPrintCoreUI2 COM 接口
description: IPrintCoreUI2 COM 接口
ms.assetid: 3c9df0ac-d823-4c27-bd34-85765f48b972
keywords:
- IPrintCoreUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d4d2f522fe96544211ee643024c70b6620e673
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543148"
---
# <a name="iprintcoreui2-com-interface"></a>IPrintCoreUI2 COM 接口





`IPrintCoreUI2` COM 接口扩展[IPrintOemDriverUI COM 接口](iprintoemdriverui-com-interface.md)。 在 Windows XP 及更高版本，Pscript5 驱动程序提供了`IPrintCoreUI2`COM 接口。 此接口中的方法是以仅供 Pscript5 UI 插件。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553036" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553036)"><strong>IPrintCoreUI2::DrvGetDriverSetting</strong></a></p></td>
<td><p>允许插件的 UI 获取打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553039" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpdateUISetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553039)"><strong>IPrintCoreUI2::DrvUpdateUISetting</strong></a></p></td>
<td><p>允许插件的 UI 来通知已修改的用户界面选项的驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553041" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpgradeRegistrySetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553041)"><strong>IPrintCoreUI2::DrvUpgradeRegistrySetting</strong></a></p></td>
<td><p>使 OEM 插件来升级私有注册表设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553045" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumConstrainedOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553045)"><strong>IPrintCoreUI2::EnumConstrainedOptions</strong></a></p></td>
<td><p>确定哪些选项的一项功能受到限制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553050" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumFeatures&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553050)"><strong>IPrintCoreUI2::EnumFeatures</strong></a></p></td>
<td><p>枚举打印机&#39;s 可用功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553052" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553052)"><strong>IPrintCoreUI2::EnumOptions</strong></a></p></td>
<td><p>枚举特定功能的可用选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553056" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetFeatureAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553056)"><strong>IPrintCoreUI2::GetFeatureAttribute</strong></a></p></td>
<td><p>检索功能特性列表或特定的功能属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553059" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetGlobalAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553059)"><strong>IPrintCoreUI2::GetGlobalAttribute</strong></a></p></td>
<td><p>检索的全局属性列表或特定的全局属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553064" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptionAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553064)"><strong>IPrintCoreUI2::GetOptionAttribute</strong></a></p></td>
<td><p>检索选项属性列表或特定的选项属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553069" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553069)"><strong>IPrintCoreUI2::GetOptions</strong></a></p></td>
<td><p>检索驱动程序&#39;中的功能/选项关键字对列表的格式的当前功能设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553074" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::QuerySimulationSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553074)"><strong>IPrintCoreUI2::QuerySimulationSupport</strong></a></p></td>
<td><p>检索后台处理程序模拟功能结构，指示的模拟后台处理程序支持的类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553081" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::SetOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553081)"><strong>IPrintCoreUI2::SetOptions</strong></a></p></td>
<td><p>设置驱动程序&#39;s 功能设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553087" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::WhyConstrained&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553087)"><strong>IPrintCoreUI2::WhyConstrained</strong></a></p></td>
<td><p>确定为什么约束指定的功能/选项选择。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




