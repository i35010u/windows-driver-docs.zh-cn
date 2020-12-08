---
title: 公开元素
description: 可选的公开元素指定文档的公开设置。
keywords:
- 公开元素图像设备
topic_type:
- apiref
api_name:
- wscn Exposure wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f3f1579530bd1610781a62fcacb2c2120b36e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822407"
---
# <a name="exposure-element"></a>公开元素


可选的 **公开** 元素指定文档的公开设置。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Exposure wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Exposure wscn:MustHonor="">
```

<a name="attributes"></a>特性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="autoexposure.md" data-raw-source="[&lt;strong&gt;AutoExposure&lt;/strong&gt;](autoexposure.md)"><strong>AutoExposure</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="exposuresettings.md" data-raw-source="[&lt;strong&gt;ExposureSettings&lt;/strong&gt;](exposuresettings.md)"><strong>ExposureSettings</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**公开** 元素可以包含 [**AutoExposure**](autoexposure.md)或 [**ExposureSettings**](exposuresettings.md)元素，但不能同时包含两者。 **AutoExposure** 指定设备应自动使用图像处理技术将文档的背景减少到白色图像。 **ExposureSettings** 指定在获取后 WSD 扫描服务应应用于图像数据的特定 **曝光** 调整值。

仅当 **曝露** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>请参阅


[**AutoExposure**](autoexposure.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






