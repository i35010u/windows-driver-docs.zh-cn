---
title: DefaultScanTicket 元素
description: 了解 "DefaultScanTicket" 元素。 查看代码示例和其他可用资源。
keywords:
- DefaultScanTicket 元素图像设备
topic_type:
- apiref
api_name:
- wscn DefaultScanTicket
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b413af0de4850d4e641a3faa68eeb5ab78ba3f8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813777"
---
# <a name="defaultscanticket-element"></a>DefaultScanTicket 元素


<a name="usage"></a>使用情况
-----

```xml
<wscn:DefaultScanTicket>
  child elements
</wscn:DefaultScanTicket>
```

<a name="attributes"></a>特性
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
<td><p><a href="elementdata-for-scannerelements-element.md" data-raw-source="[&lt;strong&gt;ElementData Element for ScannerElements&lt;/strong&gt;](elementdata-for-scannerelements-element.md)"><strong>ScannerElements 的 ElementData 元素</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DefaultScanTicket** 元素是 [**ScanTicket**](scanticket.md)元素的实例。 **DefaultScanTicket** 描述了创建作业时，WSD 扫描服务将应用的当前默认值集，而无需指定处理元素。

客户端可以通过 [**GetScannerElementsRequest**](getscannerelementsrequest.md)操作请求扫描程序的 **DefaultScanTicket** 元素，然后在通过 [**CreateScanJobRequest**](createscanjobrequest.md)操作请求扫描作业时使用该元素而不会出错。 **DefaultScanTicket** 将包含设备支持的所有 **ScanTicket** 选项的值。

<a name="examples"></a>示例
--------

下面的代码示例演示了一个示例 DefaultScanTicket。

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

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentParameters**](documentparameters.md)

[**ElementChanges**](elementchanges.md)

[**ScannerElements 的 ElementData 元素**](elementdata-for-scannerelements-element.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**JobDescription**](jobdescription.md)

[**ScanTicket**](scanticket.md)

 

 






