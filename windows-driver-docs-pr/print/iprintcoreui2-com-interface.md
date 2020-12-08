---
title: IPrintCoreUI2 COM 接口
description: IPrintCoreUI2 COM 接口
keywords:
- IPrintCoreUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 926e7445bfbb7fa945ff7a47278fe01be8a3745c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796641"
---
# <a name="iprintcoreui2-com-interface"></a>IPrintCoreUI2 COM 接口





`IPrintCoreUI2`Com 接口扩展了[IPrintOemDriverUI com 接口](iprintoemdriverui-com-interface.md)。 在 Windows XP 和更高版本中，Pscript5 驱动程序提供了 `IPrintCoreUI2` COM 接口。 此接口中的方法仅供 Pscript5 UI 插件使用。

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
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvGetDriverSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-drvgetdriversetting)"><strong>IPrintCoreUI2：:D rvGetDriverSetting</strong></a></p></td>
<td><p>允许 UI 插件获取打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-drvupdateuisetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpdateUISetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-drvupdateuisetting)"><strong>IPrintCoreUI2：:D rvUpdateUISetting</strong></a></p></td>
<td><p>允许 UI 插件通知驱动程序已修改的用户界面选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-drvupgraderegistrysetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpgradeRegistrySetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-drvupgraderegistrysetting)"><strong>IPrintCoreUI2：:D rvUpgradeRegistrySetting</strong></a></p></td>
<td><p>使 OEM 插件能够升级私有注册表设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumConstrainedOptions&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)"><strong>IPrintCoreUI2::EnumConstrainedOptions</strong></a></p></td>
<td><p>确定功能的哪些选项受到限制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumFeatures&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)"><strong>IPrintCoreUI2::EnumFeatures</strong></a></p></td>
<td><p>枚举打印机的可用功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumOptions&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)"><strong>IPrintCoreUI2::EnumOptions</strong></a></p></td>
<td><p>枚举特定功能的可用选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetFeatureAttribute&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)"><strong>IPrintCoreUI2::GetFeatureAttribute</strong></a></p></td>
<td><p>检索功能属性列表或特定功能属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetGlobalAttribute&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)"><strong>IPrintCoreUI2::GetGlobalAttribute</strong></a></p></td>
<td><p>检索全局属性列表或特定全局属性的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptionAttribute&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)"><strong>IPrintCoreUI2::GetOptionAttribute</strong></a></p></td>
<td><p>检索选项属性列表或特定选项属性的值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptions&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)"><strong>IPrintCoreUI2::GetOptions</strong></a></p></td>
<td><p>以功能/选项关键字对的列表格式检索驱动程序的当前功能设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-querysimulationsupport" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::QuerySimulationSupport&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-querysimulationsupport)"><strong>IPrintCoreUI2::QuerySimulationSupport</strong></a></p></td>
<td><p>检索后台处理程序模拟功能结构，该结构指示后台处理程序支持的模拟类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::SetOptions&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)"><strong>IPrintCoreUI2：： SetOptions</strong></a></p></td>
<td><p>设置驱动程序的功能设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::WhyConstrained&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)"><strong>IPrintCoreUI2::WhyConstrained</strong></a></p></td>
<td><p>确定指定的功能/选项选择被约束的原因。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

