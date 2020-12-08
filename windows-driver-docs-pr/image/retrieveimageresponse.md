---
title: RetrieveImageResponse 元素
description: 必需的 RetrieveImageResponse 操作元素将扫描数据返回到客户端。
keywords:
- RetrieveImageResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn RetrieveImageResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35bdcb963c2a7f343f041fc90d7334c975ee9e10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790627"
---
# <a name="retrieveimageresponse-element"></a>RetrieveImageResponse 元素


必需的 **RetrieveImageResponse** 操作元素将扫描数据返回到客户端。

<a name="usage"></a>使用情况
-----

```xml
<wscn:RetrieveImageResponse>
  child elements
</wscn:RetrieveImageResponse>
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
<td><p><a href="scandata.md" data-raw-source="[&lt;strong&gt;ScanData&lt;/strong&gt;](scandata.md)"><strong>ScanData</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持 **RetrieveImageResponse** 操作元素。 当客户端成功发送 [**RetrieveImageRequest**](retrieveimagerequest.md) 元素时，扫描服务将发送此元素。

扫描服务使用 **RetrieveImageResponse** 数据包将扫描数据返回为二进制附件。 必须将响应打包为 MIME Multipart-Related 内容类型，并使用 SOAP 消息传输优化机制 \[ MTOM \] 来有效地发送二进制图像数据。

扫描服务在生成的文件中返回的图像数取决于 [**ScanTicket**](scanticket.md)的 [**ImagesToTransfer**](imagestotransfer.md)元素和 image file [**Format**](format.md)元素的组合，如下所示：

-   如果 **format** 指定了单一图像格式，则返回的文件将始终包含一个图像。
-   如果 **Format** 指定了多页格式，则返回的文件将包含任意数量的图像，因为输入源可以扫描到 **ImagesToTransfer** 的值。

如果 [**format**](format.md) 指定单个图像格式，且 [**ImagesToTransfer**](imagestotransfer.md) 的值为0或大于1，则客户端将发送重复的 [**RetrieveImageRequest**](retrieveimagerequest.md) 操作元素，直到扫描服务使用 **ClientErrorNoImagesAvailable** 错误答复或满足 **ImagesToTransfer** 值为止。

如果在传输图像数据的过程中发生通信错误，扫描服务应中止 [**JobStateReason**](jobstatereason.md) 为 **ImageTransferError** 的作业。

<a name="examples"></a>示例
--------

下面的代码示例演示了 WSD 扫描服务如何向客户端发送图像数据。

```xml
mime-version: 1.0
Content-Type: multipart/related;
    type=application/xop+xml;
    boundary=4aa7d814-adc1-47a2-8e1c-07585b9892a4;
    start="<14629f74-2047-436c-8046-5cac76d280fc@uuid>";
    startinfo=application/soap+xml


--4aa7d814-adc1-47a2-8e1c-07585b9892a4
Content-Type: application/xop+xml; type="application/soap+xml"
                                   charset=UTF-8
Content-Transfer-Encoding: binary
Content-ID: <14629f74-2047-436c-8046-5cac76d280fc@uuid>

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="https://www.w3.org/2003/12/xop/include"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheRetrieveImageRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:RetrieveImageResponse>
      <wscn:ScanData>
        <xop:Include href="cid:1c696bd7-005a-48d9-9ee9-9adca11f8892@uuid" />
      </wscn:ScanData>
    </wscn:RetrieveImageResponse>
  </soap:Body>
</soap:Envelope>

--4aa7d814-adc1-47a2-8e1c-07585b9892a4

Content-Type: image/jpeg;
Content-Transfer-Encoding: binary
Content-ID: <1c696bd7-005a-48d9-9ee9-9adca11f8892@uuid >

Binary Scan Data
--4aa7d814-adc1-47a2-8e1c-07585b9892a4--
```

## <a name="see-also"></a>请参阅

[**形式**](format.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**JobStateReason**](jobstatereason.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

[**ScanData**](scandata.md)

[**ScanTicket**](scanticket.md)
