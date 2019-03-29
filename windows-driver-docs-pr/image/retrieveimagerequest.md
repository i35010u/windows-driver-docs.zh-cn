---
title: RetrieveImageRequest 元素
description: 所需的 RetrieveImageRequest 操作元素包含用于创建扫描作业后从设备检索扫描数据的客户端的请求。
ms.assetid: 4f6d6bd0-b323-4f95-b380-2be9cec1ee6e
keywords:
- RetrieveImageRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn RetrieveImageRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0023e7ca3f8211e5d626455ae634e983b79145c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577398"
---
# <a name="retrieveimagerequest-element"></a>RetrieveImageRequest 元素


所需**RetrieveImageRequest**操作元素包含用于创建扫描作业后从设备检索扫描数据的客户端的请求。

<a name="usage"></a>用法
-----

```xml
<wscn:RetrieveImageRequest>
  child elements
</wscn:RetrieveImageRequest>
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
<td><p><a href="documentdescription.md" data-raw-source="[&lt;strong&gt;DocumentDescription&lt;/strong&gt;](documentdescription.md)"><strong>DocumentDescription</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobtoken.md" data-raw-source="[&lt;strong&gt;JobToken&lt;/strong&gt;](jobtoken.md)"><strong>JobToken</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**RetrieveImageRequest**操作元素。

扫描服务必须验证[ **JobId** ](jobid.md)并[ **JobToken** ](jobtoken.md)客户端提供以确保该作业是有效的元素和已通过为请求检索的客户端。 如果请求是有效的扫描服务必须响应[ **RetrieveImageResponse** ](retrieveimageresponse.md)操作元素。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

此操作可能也会返回以下错误：

-   **ClientErrorJobIdNotFound**扫描程序找不到 JobId 值相匹配的作业或作业 Id 值不在定义的范围内。

    | Fault 属性 | 定义                         |
    |----------------|------------------------------------|
    | \[Code\]       | soap:Sender                        |
    | \[Subcode\]    | wscn:ClientErrorJobIdNotFound      |
    | \[Reason\]     | 找不到指定的 JobId。 |
    | \[详细信息\]     | JobId:不正确的作业 Id             |

     

-   **ClientErrorNoImagesAvailable**扫描程序不具有可用于客户端来检索任何更多映像。

    | Fault 属性 | 定义                                     |
    |----------------|------------------------------------------------|
    | \[Code\]       | soap:Sender                                    |
    | \[Subcode\]    | wscn:ClientErrorNoImagesAvailable              |
    | \[Reason\]     | 在服务器具有可用来获取任何映像。 |
    | \[详细信息\]     | 无                                           |

     

-   **ClientErrorInvalidJobToken**提供的 JobToken 值不能用于指定扫描作业 Id。

    | Fault 属性 | 定义                                                          |
    |----------------|---------------------------------------------------------------------|
    | \[Code\]       | soap:Sender                                                         |
    | \[Subcode\]    | wscn:ClientErrorInvalidJobToken                                     |
    | \[Reason\]     | JobToken 参数值使用 JobId 参数无效。 |
    | \[详细信息\]     | 无                                                                |

     

-   **ClientErrorJobCancelled**

    | Fault 属性 | 定义                              |
    |----------------|-----------------------------------------|
    | \[Code\]       | soap:Sender                             |
    | \[Subcode\]    | wscn:ClientErrorJobCancelled            |
    | \[Reason\]     | 当前扫描作业已取消。 |
    | \[详细信息\]     | 无                                    |

     

<a name="examples"></a>示例
--------

下面的代码示例显示了客户端请求来检索标识 JobId 1 的作业的图像数据。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:RetrieveImageRequest>
      <wscn:JobId>1</wscn:JobId>
      <wscn:JobToken>Job9876TokenString</wscn:JobToken>
      <wscn:DocumentDescription>
        <wscn:DocumentName>Scan001.jpg</DocumentName>
      </wscn:DocumentDescription>
    </wscn:RetrieveImageRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**DocumentDescription**](documentdescription.md)

[**JobId**](jobid.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageResponse**](retrieveimageresponse.md)

 

 






