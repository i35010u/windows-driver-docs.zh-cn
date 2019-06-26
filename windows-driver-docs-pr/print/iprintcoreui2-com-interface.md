---
title: IPrintCoreUI2 COM 接口
description: IPrintCoreUI2 COM 接口
ms.assetid: 3c9df0ac-d823-4c27-bd34-85765f48b972
keywords:
- IPrintCoreUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6fba8d8e0b9f7114afe814f8eb1407b78453d88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384188"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvgetdriversetting)"><strong>IPrintCoreUI2::DrvGetDriverSetting</strong></a></p></td>
<td><p>允许插件的 UI 获取打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupdateuisetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpdateUISetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupdateuisetting)"><strong>IPrintCoreUI2::DrvUpdateUISetting</strong></a></p></td>
<td><p>允许插件的 UI 来通知已修改的用户界面选项的驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupgraderegistrysetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpgradeRegistrySetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupgraderegistrysetting)"><strong>IPrintCoreUI2::DrvUpgradeRegistrySetting</strong></a></p></td>
<td><p>使 OEM 插件来升级私有注册表设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumConstrainedOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)"><strong>IPrintCoreUI2::EnumConstrainedOptions</strong></a></p></td>
<td><p>确定哪些选项的一项功能受到限制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumFeatures&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)"><strong>IPrintCoreUI2::EnumFeatures</strong></a></p></td>
<td><p>枚举打印机的可用功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)"><strong>IPrintCoreUI2::EnumOptions</strong></a></p></td>
<td><p>枚举特定功能的可用选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetFeatureAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)"><strong>IPrintCoreUI2::GetFeatureAttribute</strong></a></p></td>
<td><p>检索功能特性列表或特定的功能属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetGlobalAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)"><strong>IPrintCoreUI2::GetGlobalAttribute</strong></a></p></td>
<td><p>检索的全局属性列表或特定的全局属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptionAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)"><strong>IPrintCoreUI2::GetOptionAttribute</strong></a></p></td>
<td><p>检索选项属性列表或特定的选项属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)"><strong>IPrintCoreUI2::GetOptions</strong></a></p></td>
<td><p>检索驱动程序的当前功能设置中的功能/选项关键字对列表的格式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-querysimulationsupport" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::QuerySimulationSupport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-querysimulationsupport)"><strong>IPrintCoreUI2::QuerySimulationSupport</strong></a></p></td>
<td><p>检索后台处理程序模拟功能结构，指示的模拟后台处理程序支持的类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::SetOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)"><strong>IPrintCoreUI2::SetOptions</strong></a></p></td>
<td><p>设置驱动程序的功能设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::WhyConstrained&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)"><strong>IPrintCoreUI2::WhyConstrained</strong></a></p></td>
<td><p>确定为什么约束指定的功能/选项选择。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




