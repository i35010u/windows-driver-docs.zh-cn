---
title: RetrieveImageRequest 元素
description: 必需的 RetrieveImageRequest 操作元素包含客户端在创建扫描作业之后从设备检索扫描数据的请求。
keywords:
- RetrieveImageRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn RetrieveImageRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52c54ced13029458f681bb453d534d72e1281764
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790635"
---
# <a name="retrieveimagerequest-element"></a>RetrieveImageRequest 元素


必需的 **RetrieveImageRequest** 操作元素包含客户端在创建扫描作业之后从设备检索扫描数据的请求。

<a name="usage"></a>使用情况
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

WSD 扫描服务必须支持 **RetrieveImageRequest** 操作元素。

扫描服务必须验证客户端提供的 [**JobId**](jobid.md) 和 [**JobToken**](jobtoken.md) 元素，以确保作业有效并且由请求检索的客户端创建。 如果请求有效，则扫描服务必须使用 [**RetrieveImageResponse**](retrieveimageresponse.md) 操作元素进行响应。

此操作可以返回所有常见的 [**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅 [WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

此操作还可能会返回以下错误：

-   **ClientErrorJobIdNotFound** 扫描仪找不到与 JobId 值匹配的作业，或 JobId 值不在定义的范围内。

    | 错误属性 | 定义                         |
    |----------------|------------------------------------|
    | \[代码\]       | soap：发送方                        |
    | \[子代码\]    | wscn:ClientErrorJobIdNotFound      |
    | \[原因\]     | 找不到指定的 JobId。 |
    | Detail\[\]     | JobId： JobId 不正确             |

     

-   **ClientErrorNoImagesAvailable** 扫描仪没有更多可供客户端检索的映像。

    | 错误属性 | 定义                                     |
    |----------------|------------------------------------------------|
    | \[代码\]       | soap：发送方                                    |
    | \[子代码\]    | wscn:ClientErrorNoImagesAvailable              |
    | \[原因\]     | 服务器没有可获取的映像。 |
    | Detail\[\]     | 无                                           |

     

-   **ClientErrorInvalidJobToken** 对于指定的扫描 JobId，提供的 JobToken 值无效。

    | 错误属性 | 定义                                                          |
    |----------------|---------------------------------------------------------------------|
    | \[代码\]       | soap：发送方                                                         |
    | \[子代码\]    | wscn:ClientErrorInvalidJobToken                                     |
    | \[原因\]     | JobToken 参数值对于 JobId 参数无效。 |
    | Detail\[\]     | 无                                                                |

     

-   **ClientErrorJobCancelled**

    | 错误属性 | 定义                              |
    |----------------|-----------------------------------------|
    | \[代码\]       | soap：发送方                             |
    | \[子代码\]    | wscn:ClientErrorJobCancelled            |
    | \[原因\]     | 当前扫描作业已取消。 |
    | Detail\[\]     | 无                                    |

     

<a name="examples"></a>示例
--------

下面的代码示例演示了一个客户端请求，以检索由 JobId 1 标识的作业的图像数据。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/RetrieveImage
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

 

 






