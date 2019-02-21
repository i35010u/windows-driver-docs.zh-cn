---
title: ScannerElementsChangeEvent 元素
description: 所需的 ScannerElementsChangeEvent 元素告知客户端在扫描仪中已发生更改。
ms.assetid: 5a3eb934-631d-432b-befa-c67360fe68d1
keywords:
- ScannerElementsChangeEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerElementsChangeEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a89411a3bef5f92972c580ce41e37911e3531d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554213"
---
# <a name="scannerelementschangeevent-element"></a>ScannerElementsChangeEvent 元素


所需**ScannerElementsChangeEvent**元素告知客户端的扫描程序中发生了更改。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerElementsChangeEvent>
  child elements
</wscn:ScannerElementsChangeEvent>
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
<td><p><a href="elementchanges.md" data-raw-source="[&lt;strong&gt;ElementChanges&lt;/strong&gt;](elementchanges.md)"><strong>ElementChanges</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务应发送**ScannerElementsChangeEvent**向客户端时元素内已更改的元素[ **ScannerDescription**](scannerdescription.md)， [**ScannerConfiguration**](scannerconfiguration.md)， [ **DefaultScanTicket**](defaultscanticket.md)，或在扫描程序供应商扩展。

正文**ScannerElementsChangeEvent**必须包含[ **ElementChanges** ](elementchanges.md)具有已更新元素的完整 XML 元素。 如果返回的 XML 中缺少可选元素，WSD 扫描服务表示向客户端中，该服务不再支持该元素。 中支持此更改可能引起的一个选项，如电影扫描选项或双工扫描模式的删除。 客户端必须比较中的信息**ElementChanges**针对以前的数据来确定哪些值已更改，必须更新其内部数据存储。

<a name="examples"></a>示例
--------

下面的代码示例演示如何将设备报告由于扫描选项电影胶片安装更新扫描程序配置信息。

```xml
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerElementsChangeEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerElementsChangeEvent>
      <wscn:ElementChanges>
        <wscn:ScannerConfiguration>

          <wscn:DeviceSettings>
            <wscn:FormatsSupported>
              <wscn:FormatValue>dib</wscn:FormatValue>
              <wscn:FormatValue>exif</wscn:FormatValue>
              <wscn:FormatValue>jpeg2k</wscn:FormatValue>
              <wscn:FormatValue>pdf-a</wscn:FormatValue>
              <wscn:FormatValue>png</wscn:FormatValue>
              <wscn:FormatValue>tiff-single-uncompressed</wscn:FormatValue>
              <wscn:FormatValue>tiff-single-g4</wscn:FormatValue>
              <wscn:FormatValue>tiff-multi-uncompressed</wscn:FormatValue>
              <wscn:FormatValue>tiff-multi-g4</wscn:FormatValue>
              <wscn:FormatValue>xps</wscn:FormatValue>
            </wscn:FormatsSupported>
            <wscn:CompressionQualityFactorSupported>
              <wscn:MinValue>15</wscn:MinValue>
              <wscn:MaxValue>100</wscn:MaxValue>
            </wscn:CompressionQualityFactorSupported>
            <wscn:ContentTypesSupported>
              <wscn:ContentTypeValue>Auto</wscn:ContentTypeValue>
              <wscn:ContentTypeValue>Text</wscn:ContentTypeValue>
              <wscn:ContentTypeValue>Photo</wscn:ContentTypeValue>
              <wscn:ContentTypeValue>Halftone</wscn:ContentTypeValue>
              <wscn:ContentTypeValue>Mixed</wscn:ContentTypeValue>
            </wscn:ContentTypesSupported>
            <wscn:DocumentSizeAutoDetectSupported>
              true
            </wscn:DocumentSizeAutoDetectSupported>
            <wscn:AutoExposureSupported>true</wscn:AutoExposureSupported>
            <wscn:BrightnessSupported>true</wscn:BrightnessSupported>
            <wscn:ContrastSupported>true</wscn:ContrastSupported>
            <wscn:ScalingRangeSupported>
              <wscn:ScalingWidth>
                <wscn:MinValue>50</wscn:MinValue>
                <wscn:MaxValue>500</wscn:MaxValue>
              </wscn:ScalingWidth>
              <wscn:ScalingHeight>
                <wscn:MinValue>50</wscn:MinValue>
                <wscn:MaxValue>500</wscn:MaxValue>
              </wscn:ScalingHeight>
            </wscn:ScalingRangeSupported>
            <wscn:RotationsSupported>
              <wscn:RotationValue>0</wscn:RotationValue>
              <wscn:RotationValue>90</wscn:RotationValue>
              <wscn:RotationValue>180</wscn:RotationValue>
              <wscn:RotationValue>270</wscn:RotationValue>
            </wscn:RotationsSupported>
          </wscn:DeviceSettings>

          <wscn:Platen>
            <wscn:PlatenOpticalResolution>
              <wscn:Width>1200</wscn:Width>
              <wscn:Height>1200</wscn:Height>
            </wscn:PlatenOpticalResolution>
            <wscn:PlatenResolutions>
              <wscn:Widths>
                <wscn:Width>150</wscn:Width>
                <wscn:Width>204</wscn:Width>
                <wscn:Width>300</wscn:Width>
                <wscn:Width>600</wscn:Width>
                <wscn:Width>1200</wscn:Width>
              </wscn:Widths>
              <wscn:Heights>
                <wscn:Height>96</wscn:Height>
                <wscn:Height>150</wscn:Height>
                <wscn:Height>204</wscn:Height>
                <wscn:Height>300</wscn:Height>
                <wscn:Height>600</wscn:Height>
                <wscn:Height>900</wscn:Height>
                <wscn:Height>1200</wscn:Height>
              </wscn:Heights>
            </wscn:PlatenResolutions>
            <wscn:PlatenColor>
              <wscn:ColorEntry>BlackAndWhite1</wscn:ColorEntry>
              <wscn:ColorEntry>Grayscale4</wscn:ColorEntry>
              <wscn:ColorEntry>Grayscale8</wscn:ColorEntry>
              <wscn:ColorEntry>RGB24</wscn:ColorEntry>
              <wscn:ColorEntry>RGB48</wscn:ColorEntry>
              <wscn:ColorEntry>RGBa32</wscn:ColorEntry>
              <wscn:ColorEntry>RGBa64</wscn:ColorEntry>
            </wscn:PlatenColor>
            <wscn:PlatenMinimumSize>
              <wscn:Width>250</wscn:Width>
              <wscn:Height>250</wscn:Height>
            </wscn:PlatenMinimumSize>
            <wscn:PlatenMaximumSize>
              <wscn:Width>11000</wscn:Width>
              <wscn:Height>14000</wscn:Height>
            </wscn:PlatenMaximumSize>
          </wscn:Platen>

          <wscn:ADF>
            <wscn:ADFSupportsDuplex>false</wscn:ADFSupportsDuplex>
            <wscn:ADFFront>
              <wscn:ADFOpticalResolution>
                <wscn:Width>600</wscn:Width>
                <wscn:Height>600</wscn:Height>
              </wscn:ADFOpticalResolution>
              <wscn:ADFResolutions>
                <wscn:Widths>
                  <wscn:Width>150</wscn:Width>
                  <wscn:Width>204</wscn:Width>
                  <wscn:Width>300</wscn:Width>
                  <wscn:Width>600</wscn:Width>
                </wscn:Widths>
                <wscn:Heights>
                  <wscn:Height>96</wscn:Height>
                  <wscn:Height>150</wscn:Height>
                  <wscn:Height>204</wscn:Height>
                  <wscn:Height>300</wscn:Height>
                  <wscn:Height>600</wscn:Height>
                </wscn:Heights>
              </wscn:ADFResolutions>
              <wscn:ADFColor>
                <wscn:ColorEntry>BlackAndWhite1</wscn:ColorEntry>
                <wscn:ColorEntry>Grayscale4</wscn:ColorEntry>
                <wscn:ColorEntry>RGB24</wscn:ColorEntry>
              </wscn:ADFColor>
              <wscn:ADFMinimumSize>
                <wscn:Width>4000</wscn:Width>
                <wscn:Height>6000</wscn:Height>
              </wscn:ADFMinimumSize>
              <wscn:ADFMaximumSize>
                <wscn:Width>8500</wscn:Width>
                <wscn:Height>11000</wscn:Height>
              </wscn:ADFMaximumSize>
            </wscn:ADFFront>
          </wscn:ADF>

          <wscn:Film>
            <wscn:FilmScanModesSupported>
              <wscn:FilmScanModeValue>
                ColorSlideFilm
              </wscn:FilmScanModeValue>
              <wscn:FilmScanModeValue>
                ColorNegativeFilm
              </wscn:FilmScanModeValue>
              <wscn:FilmScanModeValue>
                BlackandWhiteNegativeFilm
              </wscn:FilmScanModeValue>
            </wscn:FilmScanModesSupported>
            <wscn:FilmOpticalResolution>
              <wscn:Width>600</wscn:Width>
              <wscn:Height>600</wscn:Height>
            </wscn:FilmOpticalResolution>
            <wscn:FilmResolutions>
              <wscn:Widths>
                <wscn:Width>150</wscn:Width>
                <wscn:Width>300</wscn:Width>
                <wscn:Width>600</wscn:Width>
              </wscn:Widths>
              <wscn:Heights>
                <wscn:Height>150</wscn:Height>
                <wscn:Height>300</wscn:Height>
                <wscn:Height>600</wscn:Height>
              </wscn:Heights>
            </wscn:FilmResolutions>
            <wscn:FilmColor>
              <wscn:ColorEntry>BlackAndWhite1</wscn:ColorEntry>
              <wscn:ColorEntry>Grayscale4</wscn:ColorEntry>
              <wscn:ColorEntry>RGB24</wscn:ColorEntry>
              <wscn:ColorEntry>RGBa32</wscn:ColorEntry>
            </wscn:FilmColor>
            <wscn:FilmMinimumSize>
              <wscn:Width>1378</wscn:Width>
              <wscn:Height>1378</wscn:Height>
            </wscn:FilmMinimumSize>
            <wscn:FilmMaximumSize>
              <wscn:Width>2756</wscn:Width>
              <wscn:Height>10000</wscn:Height>
            </wscn:FilmMaximumSize>
          </wscn:Film>

        </wscn:ScannerConfiguration>
      </wscn:ElementChanges>
    </wscn:ScannerElementsChangeEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>另请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**ElementChanges**](elementchanges.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

 

 






