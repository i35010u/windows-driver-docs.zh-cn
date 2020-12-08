---
title: ScannerElementsChangeEvent 元素
description: 必需的 ScannerElementsChangeEvent 元素将通知客户端已在扫描仪中发生了更改。
keywords:
- ScannerElementsChangeEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerElementsChangeEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6c4bddf7712914734250fabedaf9b6ec1f074b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813759"
---
# <a name="scannerelementschangeevent-element"></a>ScannerElementsChangeEvent 元素


必需的 **ScannerElementsChangeEvent** 元素将通知客户端已在扫描仪中发生了更改。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerElementsChangeEvent>
  child elements
</wscn:ScannerElementsChangeEvent>
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
<td><p><a href="elementchanges.md" data-raw-source="[&lt;strong&gt;ElementChanges&lt;/strong&gt;](elementchanges.md)"><strong>ElementChanges</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

当某个元素在扫描仪中的 [**ScannerDescription**](scannerdescription.md)、 [**ScannerConfiguration**](scannerconfiguration.md)、 [**DefaultScanTicket**](defaultscanticket.md)或供应商扩展中发生更改时，WSD 扫描服务应将 **ScannerElementsChangeEvent** 元素发送到客户端。

**ScannerElementsChangeEvent** 的主体必须包含一个 [**ElementChanges**](elementchanges.md)元素，该元素具有更新的元素的完整 XML。 如果返回的 XML 中缺少一个可选元素，则 WSD 扫描服务将向客户端指示该服务不再支持该元素。 此支持更改可能是由于删除了某个选项（如胶卷扫描选项或双工扫描模式）引起的。 客户端必须对 **ElementChanges** 中的信息与以前的数据进行比较，以确定哪些值已更改并且必须更新其内部数据存储。

<a name="examples"></a>示例
--------

下面的代码示例演示设备如何报告更新的扫描程序配置信息，因为安装了胶片扫描选项。

```xml
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerElementsChangeEvent
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

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**ElementChanges**](elementchanges.md)

[**ScannerConfiguration**](scannerconfiguration.md)

[**ScannerDescription**](scannerdescription.md)

 

 






