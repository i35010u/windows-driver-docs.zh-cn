---
title: DefaultScanTicket 元素
description: .
ms.assetid: 1c0f15c8-b14f-4607-8655-36e1397082e6
keywords:
- DefaultScanTicket 元素成像设备
topic_type:
- apiref
api_name:
- wscn DefaultScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 653d82cba1a9f68ddea76f0a124482c263b1ceea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543898"
---
# <a name="defaultscanticket-element"></a>DefaultScanTicket 元素


<a name="usage"></a>用法
-----

```xml
<wscn:DefaultScanTicket>
  child elements
</wscn:DefaultScanTicket>
```

<a name="attributes"></a>属性
----------

没有特性。

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
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
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
<td><p><a href="elementchanges.md" data-raw-source="[&lt;strong&gt;ElementChanges&lt;/strong&gt;](elementchanges.md)"><strong>ElementChanges</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="elementdata-for-scannerelements-element.md" data-raw-source="[&lt;strong&gt;ElementData Element for ScannerElements&lt;/strong&gt;](elementdata-for-scannerelements-element.md)"><strong>ScannerElements ElementData 元素</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DefaultScanTicket**元素是实例[ **ScanTicket** ](scanticket.md)元素。 **DefaultScanTicket**描述的默认值时不包含特定的处理元素创建一个作业，WSD 扫描服务要应用于当前集。

客户端可以请求的扫描程序**DefaultScanTicket**通过元素[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作以及如何将它不会出错请求时扫描通过作业[ **CreateScanJobRequest** ](createscanjobrequest.md)操作。 **DefaultScanTicket**将包含的所有值**ScanTicket**设备支持的选项。

<a name="examples"></a>示例
--------

下面的代码示例显示了示例 DefaultScanTicket。

```xml
<wscn:DefaultScanTicket>
  <wscn:JobDescription>
    <wscn:JobName>Scan Job</wscn:JobName>
    <wscn:JobOriginatingUserName></wscn:JobOriginatingUserName>
    <wscn:JobInformation>User Selected Scan Job</wscn:JobInformation>
  </wscn:JobDescription>
  <wscn:DocumentParameters>
    <wscn:Format>tiff-multi-uncompressed</wscn:Format>
    <wscn:CompressionQualityFactor>100</wscn:CompressionQualityFactor>
    <wscn:ImagesToTransfer>0</wscn:ImagesToTransfer>
    <wscn:InputSource>Platen</wscn:InputSource>
    <wscn:FilmScanMode>NotApplicable</wscn:FilmScanMode>
    <wscn:ContentType>Auto</wscn:ContentType>
    <wscn:InputSize>
      <wscn:InputMediaSize>
      <wscn:Width>8500</wscn:Width>
      <wscn:Height>11000</wscn:Height>
      </wscn:InputMediaSize>
    </wscn:InputSize>
    <wscn:Exposure>
      <wscn:AutoExposure>true</wscn:AutoExposure>
    </wscn:Exposure>
    <wscn:Scaling>
      <wscn:ScalingWidth>100</wscn:ScalingWidth>
      <wscn:ScalingHeight>100</wscn:ScalingHeight>
    </wscn:Scaling>
    <wscn:Rotation>0</wscn:Rotation>
    <wscn:MediaSides>
      <wscn:MediaFront>
        <wscn:ScanRegion>
          <wscn:ScanRegionXOffset>0</wscn:ScanRegionXOffset>
          <wscn:ScanRegionYOffset>0</wscn:ScanRegionYOffset>
          <wscn:ScanRegionWidth>8500</wscn:ScanRegionWidth>
          <wscn:ScanRegionHeight>11000</wscn:ScanRegionHeight>
        </wscn:ScanRegion>
        <wscn:ColorProcessing>RGB24</wscn:ColorProcessing>
        <wscn:Resolution>
          <wscn:Width>600</wscn:Width>
          <wscn:Height>600</wscn:Height>
        </wscn:Resolution>
      </wscn:MediaFront>
    </wscn:MediaSides>
  </wscn:DocumentParameters>
</wscn:DefaultScanTicket>
```

## <a name="see-also"></a>另请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentParameters**](documentparameters.md)

[**ElementChanges**](elementchanges.md)

[**ScannerElements ElementData 元素**](elementdata-for-scannerelements-element.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**JobDescription**](jobdescription.md)

[**ScanTicket**](scanticket.md)

 

 






