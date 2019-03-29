---
title: RetrieveImageResponse 元素
description: 所需的 RetrieveImageResponse 操作元素返回到客户端扫描数据。
ms.assetid: f63398c4-bbae-42ca-94c5-059b066c65cb
keywords:
- RetrieveImageResponse 元素成像设备
topic_type:
- apiref
api_name:
- wscn RetrieveImageResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 225908d15af4b9e1c0e37427e82e8b5d76e8aece
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563876"
---
# <a name="retrieveimageresponse-element"></a>RetrieveImageResponse 元素


所需**RetrieveImageResponse**操作元素将扫描数据返回到客户端。

<a name="usage"></a>用法
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

WSD 扫描服务必须支持**RetrieveImageResponse**操作元素。 扫描服务会发送此元素时客户端成功发送[ **RetrieveImageRequest** ](retrieveimagerequest.md)元素。

扫描服务返回的扫描数据以与二进制附件**RetrieveImageResponse**数据包。 响应必须打包为 MIME 多部分相关的内容类型并使用的 SOAP 消息传输优化机制\[MTOM\]高效地发送二进制图像数据。

扫描服务返回的结果文件中的映像数量取决于的组合[ **ImagesToTransfer** ](imagestotransfer.md)元素[ **ScanTicket**](scanticket.md)和图像文件[**格式**](format.md)元素，如下所示：

-   如果**格式**指定单个映像格式，则返回的文件将始终包含的单一映像。
-   如果**格式**指定的多页格式，则返回的文件将包含最多的值可以扫描输入的源的尽可能多的映像**ImagesToTransfer**。

如果[**格式**](format.md)单个图像格式的值指定[ **ImagesToTransfer** ](imagestotransfer.md)是 0 或大于 1，客户端将发送重复[ **RetrieveImageRequest** ](retrieveimagerequest.md)之前使用的扫描服务回复的 operation 元素**ClientErrorNoImagesAvailable**容错或直到**ImagesToTransfer**满足值。

扫描服务应中止与作业[ **JobStateReason** ](jobstatereason.md)的**ImageTransferError**图像数据传输过程中如果有通信错误。

<a name="examples"></a>示例
--------

下面的代码示例演示如何 WSD 扫描服务将图像数据发送给客户端。

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
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="http://www.w3.org/2003/12/xop/include"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
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

[**Format**](format.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**JobStateReason**](jobstatereason.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

[**ScanData**](scandata.md)

[**ScanTicket**](scanticket.md)
