---
title: 常规 WIA 实用程序函数
description: 常规 WIA 实用程序函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a913fa78698a2881a958acbecacf4949d069a798
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808233"
---
# <a name="general-wia-utility-functions"></a>常规 WIA 实用程序函数





你可以使用以下函数来检索驱动程序项上下文、从系统注册表中检索信息并复制字符串。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetdrvitemcontext" data-raw-source="[&lt;strong&gt;wiauGetDrvItemContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetdrvitemcontext)"><strong>wiauGetDrvItemContext</strong></a></p></td>
<td><p>获取驱动程序项上下文和驱动程序项（可选）。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetresourcestring" data-raw-source="[&lt;strong&gt;wiauGetResourceString&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetresourcestring)"><strong>wiauGetResourceString</strong></a></p></td>
<td><p>获取资源字符串，并将其存储为 <strong>BSTR</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetvalidformats" data-raw-source="[&lt;strong&gt;wiauGetValidFormats&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaugetvalidformats)"><strong>wiauGetValidFormats</strong></a></p></td>
<td><p>使用指定的 TYMED 值，调用 <a href="/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"><strong>IWiaMiniDrv：:D rvgetwiaformatinfo</strong></a> 方法，并创建有效格式的列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropinpropspec" data-raw-source="[&lt;strong&gt;wiauPropInPropSpec&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropinpropspec)"><strong>wiauPropInPropSpec</strong></a></p></td>
<td><p>确定)  (ID 是否包含在此类值的数组中。 函数可以选择获取在其中找到属性规范 ID 的索引。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropsinpropspec" data-raw-source="[&lt;strong&gt;wiauPropsInPropSpec&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaupropsinpropspec)"><strong>wiauPropsInPropSpec</strong></a></p></td>
<td><p>确定属性规范 Id 列表中是否包含在此类值的数组中。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetdwordw" data-raw-source="[&lt;strong&gt;wiauRegGetDword&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetdwordw)"><strong>wiauRegGetDword</strong></a></p></td>
<td><p>获取注册表的<strong>DeviceData</strong>部分中的<strong>DWORD</strong>值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetstrw" data-raw-source="[&lt;strong&gt;wiauRegGetStr&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaureggetstrw)"><strong>wiauRegGetStr</strong></a></p></td>
<td><p>从注册表的 <strong>DeviceData</strong> 节获取字符串值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiauregopendataw" data-raw-source="[&lt;strong&gt;wiauRegOpenData&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiauregopendataw)"><strong>wiauRegOpenData</strong></a></p></td>
<td><p>打开 <strong>DeviceData</strong> 注册表项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiausetimageitemsize" data-raw-source="[&lt;strong&gt;wiauSetImageItemSize&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiausetimageitemsize)"><strong>wiauSetImageItemSize</strong></a></p></td>
<td><p>计算图像的大小和宽度（以字节为单位），它基于当前 WIA_IPA_FORMAT 设置 (在 Microsoft Windows SDK 文档) 中定义，并将新值写入适当的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2c" data-raw-source="[&lt;strong&gt;wiauStrC2C&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2c)"><strong>wiauStrC2C</strong></a></p></td>
<td><p>将 ANSI 字符串复制到另一个 ANSI 字符字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2w" data-raw-source="[&lt;strong&gt;wiauStrC2W&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrc2w)"><strong>wiauStrC2W</strong></a></p></td>
<td><p>将 ANSI 字符串转换为 Unicode 字符串。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2c" data-raw-source="[&lt;strong&gt;wiauStrW2C&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2c)"><strong>wiauStrW2C</strong></a></p></td>
<td><p>将 Unicode 字符串转换为 ANSI 字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2w" data-raw-source="[&lt;strong&gt;wiauStrW2W&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaustrw2w)"><strong>wiauStrW2W</strong></a></p></td>
<td><p>将 Unicode 字符串复制到另一个 Unicode 字符串。</p></td>
</tr>
</tbody>
</table>

 

