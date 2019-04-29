---
title: CreateScanJobRequest 元素
description: 所需的 CreateScanJobRequest 操作准备要扫描的扫描设备。
ms.assetid: ce3aafe2-71b0-4875-852a-f3ab78684329
keywords:
- CreateScanJobRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn CreateScanJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8221ab8d8df854c6a32b280ab29898afd21e196a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368545"
---
# <a name="createscanjobrequest-element"></a>CreateScanJobRequest 元素


所需**CreateScanJobRequest**扫描设备扫描准备操作。

<a name="usage"></a>用法
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

WSD 扫描服务必须支持**CreateScanJobRequest**操作。

**CreateScanJobRequest**操作是准备要扫描可供其映像的扫描设备的主要机制。 可以在两个不同的方法启动此操作。 每个方法会将发送到不同的参数**CreateScanJobRequest**。 两个方法和参数是：

-   用户选择目标，并在设备上推送扫描按钮。 在此方法中，客户端发送**CreateScanJobRequest**具有以下子元素：
    -   扫描服务将返回到客户端通过 ScanAvailableEvent ScanIdentifier 元素。 扫描服务应检查以确保用户已选定目标之后，请求正确的客户端扫描此标识符。
    -   若要接收 ScanAvailableEvent 事件在其订阅时，WSD 扫描服务将返回到客户端 DestinationToken 元素。 扫描服务应检查正确的客户端请求通过检查此令牌扫描。
    -   若要控制处理的扫描 ScanTicket 元素。 扫描票证中的值是之前用户转到设备以启动扫描在客户端设置的默认值。
-   用户在客户端上启动应用程序，并获取图像。 在此方法中，客户端发送**CreateScanJobRequest**仅含**ScanTicket**元素。

中的某些元素**CreateScanJobRequest**层次结构可以包含**MustHonor**的布尔值属性。 如果**MustHonor**是否存在并且为 true，WSD 扫描服务必须遵循所请求的元素和其值或拒绝扫描作业请求。 如果不受支持的元素不具有**MustHonor**属性，或者，如果其**MustHonor**属性为 false，WSD 扫描服务必须忽略它。 如果支持的元素**MustHonor**属性为 false，WSD 扫描服务必须 substitue 用一个支持请求的值。

如果客户端提供冲突在扫描作业请求中的元素的组合 (如[ **InputSource** ](inputsource.md)并[**解析**](resolution.md))，如果有冲突的元素，WSD 扫描服务必须拒绝扫描作业请求**MustHonor**属性值为 true。

下列元素可以具有**MustHonor**属性：[**ColorProcessing**](colorprocessing.md)， [ **CompressionQualityFactor**](compressionqualityfactor.md)， [ **ContentType**](contenttype.md)， [**暴露**](exposure.md)， [ **FilmScanMode**](filmscanmode.md)， [ **ImagesToTransfer** ](imagestotransfer.md)[ **InputSize**](inputsize.md)， [ **InputSource**](inputsource.md)， [ **MediaSides** ](mediasides.md)， [**解析**](resolution.md)， [**旋转**](rotation.md)， [**缩放** ](scaling.md)， [ **ScanRegionHeight**](scanregionheight.md)， [ **ScanRegionWidth**](scanregionwidth.md)， [**ScanRegionXOffset**](scanregionxoffset.md)，和[ **ScanRegionYOffset**](scanregionyoffset.md)。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

**CreateScanJobRequest**还可以返回以下错误：

-   **ServerErrorNotAcceptingJobs**服务器无法接受新的扫描作业。 由于已将扫描程序放入服务模式或没有用户干预条件和已用完所有内存缓冲区，则可能会出现此错误。 客户端的假定条件下，服务器已不再受阻止，扫描程序将会再次接受作业的时间可以尝试再次在以后某个时刻未经修改的请求。

    | Fault 属性 | 定义                                                                         |
    |----------------|------------------------------------------------------------------------------------|
    | \[Code\]       | soap:Receiver                                                                      |
    | \[Subcode\]    | wscn:ServerErrorNotAcceptingJobs                                                   |
    | \[Reason\]     | 该服务暂时阻止并不能接受新作业或文档的请求。 |
    | \[详细信息\]     | 无                                                                               |

     

-   **ClientErrorFormatNotSupported**扫描程序不支持所提供的格式值。

    | Fault 属性 | 定义                                                                                                                                      |
    |----------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[Code\]       | soap:Sender                                                                                                                                     |
    | \[Subcode\]    | wscn:ClientErrorFormatNotSupported                                                                                                              |
    | \[Reason\]     | 不支持的文档格式参数值。                                                                                           |
    | \[详细信息\]     | 可选。 扫描服务可以返回支持的格式列表。 此元素中的数据应为类型&lt;wscn:FormatSupportedType&gt;。 |

     

-   **ClientErrorInvalidScanIdentifier**提供的 ScanIdentifier 值不是当前有效的扫描设备中。

    | Fault 属性 | 定义                                                 |
    |----------------|------------------------------------------------------------|
    | \[Code\]       | soap:Sender                                                |
    | \[Subcode\]    | wscn:ClientErrorInvalidScanIdentifier                      |
    | \[Reason\]     | ScanIdentifier 参数值不是当前有效的。 |
    | \[详细信息\]     | 无                                                       |

     

-   **ClientErrorInvalidDestinationToken**扫描设备提供的 DestinationToken 值无效。

    | Fault 属性 | 定义                                                   |
    |----------------|--------------------------------------------------------------|
    | \[Code\]       | soap:Sender                                                  |
    | \[Subcode\]    | wscn:ClientErrorInvalidDestinationToken                      |
    | \[Reason\]     | DestinationToken 参数值不是当前有效的。 |
    | \[详细信息\]     | 无                                                         |

     

-   **ClientErrorNoImagesAvailable**服务器无法接受新的扫描作业，因为没有要扫描的媒体。 例如，从附加到扫描程序，自动文档送纸器执行扫描作业和送纸器为空时，会生成此错误。 客户端可以稍后再试未修改的请求，已固定条件和扫描程序现在具有要扫描的媒体的假定条件下产生负面影响。

    | Fault 属性 | 定义                                     |
    |----------------|------------------------------------------------|
    | \[Code\]       | soap:Sender                                    |
    | \[Subcode\]    | wscn:ClientErrorNoImagesAvailable              |
    | \[Reason\]     | 在服务器具有可用来获取任何映像。 |
    | \[详细信息\]     | 无                                           |

     

<a name="examples"></a>示例
--------

下面的代码示例显示了在从扫描设备启动扫描时扫描作业请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
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

下面的代码示例显示了在从客户端上的应用程序启动扫描时扫描作业请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
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

[**风险**](exposure.md)

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

 

 






