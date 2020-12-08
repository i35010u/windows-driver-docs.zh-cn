---
title: CreateScanJobRequest 元素
description: 必需的 CreateScanJobRequest 操作使扫描设备准备扫描。
keywords:
- CreateScanJobRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn CreateScanJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f12f8b41a84341be7d0a377ecb91e179c5f2595
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783905"
---
# <a name="createscanjobrequest-element"></a>CreateScanJobRequest 元素


必需的 **CreateScanJobRequest** 操作使扫描设备准备扫描。

<a name="usage"></a>使用情况
-----

```xml
<wscn:CreateScanJobRequest>
  child elements
</wscn:CreateScanJobRequest>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

无

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
<td><p><a href="destinationtoken.md" data-raw-source="[&lt;strong&gt;DestinationToken&lt;/strong&gt;](destinationtoken.md)"><strong>DestinationToken</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanidentifier.md" data-raw-source="[&lt;strong&gt;ScanIdentifier&lt;/strong&gt;](scanidentifier.md)"><strong>ScanIdentifier</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持 **CreateScanJobRequest** 操作。

**CreateScanJobRequest** 操作是准备扫描设备以扫描可用于它的映像的主要机制。 可以通过两种不同的方法启动此操作。 每个方法都将向 **CreateScanJobRequest** 发送不同的参数。 这两个方法和参数是：

-   用户选择一个目标并将扫描按钮推送到设备上。 在此方法中，客户端发送具有以下子元素的 **CreateScanJobRequest** ：
    -   扫描服务通过 ScanAvailableEvent 返回给客户端的 ScanIdentifier 元素。 扫描服务应检查此标识符，以确保在用户选择目标后正确的客户端请求扫描。
    -   WSD 扫描服务在订阅接收 ScanAvailableEvent 事件时返回给客户端的 DestinationToken 元素。 扫描服务应通过检查此令牌来检查正确的客户端是否正在请求扫描。
    -   用于控制扫描处理的 ScanTicket 元素。 扫描票证中的值是在用户进入设备以启动扫描之前在客户端上设置的默认值。
-   用户在客户端上启动应用程序，并获取映像。 在此方法中，客户端只发送 **CreateScanJobRequest** 的 **ScanTicket** 元素。

**CreateScanJobRequest** 层次结构中的某些元素可以包含 **MustHonor** 布尔属性。 如果 **MustHonor** 存在且为 true，则 WSD 扫描服务必须服从请求的元素及其值或拒绝扫描作业请求。 如果不受支持的元素没有 **MustHonor** 属性，或其 **MustHonor** 属性为 False，则 WSD 扫描服务必须将其忽略。 如果支持的元素的 **MustHonor** 属性为 false，则 WSD 扫描服务必须使用受支持的值记得请求的值。

如果客户端提供了扫描作业请求中的元素冲突组合 (例如 [**InputSource**](inputsource.md) 和 [**解析**](resolution.md)) ，则在发生冲突的元素的 **MustHonor** 属性值为 true 时，WSD 扫描服务必须拒绝扫描作业请求。

以下元素可以具有 **MustHonor** 属性： [**ColorProcessing**](colorprocessing.md)、 [**CompressionQualityFactor**](compressionqualityfactor.md)、 [**ContentType**](contenttype.md)、 [**曝光度**](exposure.md)、 [**FilmScanMode**](filmscanmode.md)、 [**ImagesToTransfer**](imagestotransfer.md)、 [**InputSize**](inputsize.md)、 [**InputSource**](inputsource.md)、 [**MediaSides**](mediasides.md)、 [**分辨率**](resolution.md)、 [**旋转**](rotation.md)、 [**缩放**](scaling.md)、 [**ScanRegionHeight**](scanregionheight.md)、 [**ScanRegionWidth**](scanregionwidth.md)、 [**ScanRegionXOffset**](scanregionxoffset.md)和 [**ScanRegionYOffset**](scanregionyoffset.md)。

此操作可以返回所有常见的 [**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅 [WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

**CreateScanJobRequest** 也可以返回以下错误：

-   **ServerErrorNotAcceptingJobs** 服务器无法接受新的扫描作业。 发生此错误的原因可能是扫描程序已进入服务模式，或由于用户干预条件和所有内存缓冲区均已耗尽。 客户端可以在某个以后的某个时间点再次尝试未修改的请求，并期望服务器已取消阻止并且扫描程序再次接受作业。

    | 错误属性 | 定义                                                                         |
    |----------------|------------------------------------------------------------------------------------|
    | \[代码\]       | soap：接收方                                                                      |
    | \[子代码\]    | wscn:ServerErrorNotAcceptingJobs                                                   |
    | \[原因\]     | 该服务暂时被阻止，无法接受新的作业或文档请求。 |
    | Detail\[\]     | 无                                                                               |

     

-   **ClientErrorFormatNotSupported** 扫描程序不支持提供的格式值。

    | 错误属性 | 定义                                                                                                                                      |
    |----------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[代码\]       | soap：发送方                                                                                                                                     |
    | \[子代码\]    | wscn:ClientErrorFormatNotSupported                                                                                                              |
    | \[原因\]     | 文档格式参数值不受支持。                                                                                           |
    | Detail\[\]     | 可选。 扫描服务可以返回受支持格式的列表。 此元素中的数据应为 &lt; wscn： FormatSupportedType 类型 &gt; 。 |

     

-   **ClientErrorInvalidScanIdentifier** 所提供的 ScanIdentifier 值当前在扫描设备中无效。

    | 错误属性 | 定义                                                 |
    |----------------|------------------------------------------------------------|
    | \[代码\]       | soap：发送方                                                |
    | \[子代码\]    | wscn:ClientErrorInvalidScanIdentifier                      |
    | \[原因\]     | ScanIdentifier 参数值当前无效。 |
    | Detail\[\]     | 无                                                       |

     

-   **ClientErrorInvalidDestinationToken** 提供的 DestinationToken 值对扫描设备无效。

    | 错误属性 | 定义                                                   |
    |----------------|--------------------------------------------------------------|
    | \[代码\]       | soap：发送方                                                  |
    | \[子代码\]    | wscn:ClientErrorInvalidDestinationToken                      |
    | \[原因\]     | DestinationToken 参数值当前无效。 |
    | Detail\[\]     | 无                                                         |

     

-   **ClientErrorNoImagesAvailable** 服务器无法接受新的扫描作业，因为没有要扫描的媒体。 例如，当从附加到扫描仪的自动文档送纸器执行扫描作业，并且送纸器为空时，会生成此错误。 客户端可以在以后再次尝试未修改的请求，并假定已修复条件，并且现在扫描程序有要扫描的媒体。

    | 错误属性 | 定义                                     |
    |----------------|------------------------------------------------|
    | \[代码\]       | soap：发送方                                    |
    | \[子代码\]    | wscn:ClientErrorNoImagesAvailable              |
    | \[原因\]     | 服务器没有可获取的映像。 |
    | Detail\[\]     | 无                                           |

     

<a name="examples"></a>示例
--------

下面的代码示例演示了从扫描设备启动扫描时的扫描作业请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:CreateScanJobRequest>
      <wscn:ScanIdentifier>
        uuid:12e7a983-1034-5428-d298-0016f11097fa
      </wscn:ScanIdentifier>
      <wscn:DestinationToken>
        Dest1234TokenString
      </wscn:DestinationToken>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Photo Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>jfif</wscn:Format>
          <wscn:CompressionQualityFactor>45</wscn:CompressionQualityFactor>
          <wscn:InputSource>Platen</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:DocumentSizeAutoDetect>true</wscn:DocumentSizeAutoDetect>
          </wscn:InputSize>
          <wscn:Scaling wscn:MustHonor="1">
            <wscn:ScalingWidth>125</wscn:ScalingWidth>
            <wscn:ScalingHeight>125</wscn:ScalingHeight>
          </wscn:Scaling>
          <wscn:MediaSides>
            <wscn:MediaFront>
              <wscn:Resolution wscn:MustHonor="1">
                <wscn:Width>300</wscn:Width>
                <wscn:Height>300</wscn:Height>
              </wscn:Resolution>
            </wscn:MediaFront>
          </wscn:MediaSides>
        </wscn:DocumentParameters>
      </wscn:ScanTicket>
    </wscn:CreateScanJobRequest>
  </soap:Body>
</soap:Envelope>
```

下面的代码示例显示了从客户端上的应用程序启动扫描时的扫描作业请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:CreateScanJobRequest>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Application Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>xps</wscn:Format>
          <wscn:ImagesToTransfer>0</wscn:ImagesToTransfer>
          <wscn:InputSource>ADF</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:DocumentSizeAutoDetect>true</wscn:DocumentSizeAutoDetect>
          </wscn:InputSize>
          <wscn:MediaSides>
            <wscn:MediaFront>
              <wscn:ColorProcessing>RGB48</wscn:ColorProcessing>
              <wscn:Resolution>
                <wscn:Width>1200</wscn:Width>
              </wscn:Resolution>
            </wscn:MediaFront>
          </wscn:MediaSides>
        </wscn:DocumentParameters>
        <wscn:DocumentDescription>
          <wscn:DocumentName>Scan001.jpg</DocumentName>
        </wscn:DocumentDescription>
      </wscn:ScanTicket>
    </wscn:CreateScanJobRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**ColorProcessing**](colorprocessing.md)

[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**DestinationToken**](destinationtoken.md)

[**隐患**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**InputSource**](inputsource.md)

[**MediaSides**](mediasides.md)

[**解决方法**](resolution.md)

[**旋转**](rotation.md)

[**缩放**](scaling.md)

[**ScanAvailableEvent**](scanavailableevent.md)

[**ScanIdentifier**](scanidentifier.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

[**ScanTicket**](scanticket.md)

 

 






