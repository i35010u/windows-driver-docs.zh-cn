---
title: IPrinterBidiSchemaResponses 接口
description: IPrinterBidiSchemaResponses 接口表示由 USB 双向扩展 JavaScript 方法 getSchemas 和 getStatus 填充的双向响应集。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 2E68C4AA-D235-46D2-81D6-D6C7E84C2FEF
keywords:
- IPrinterBidiSchemaResponses 接口打印设备
- IPrinterBidiSchemaResponses 接口打印设备，描述
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2daa0bf1731c3ce18692b70b388f16f9f9ad30c3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218207"
---
# <a name="iprinterbidischemaresponses-interface"></a>IPrinterBidiSchemaResponses 接口

IPrinterBidiSchemaResponses 接口表示由 USB 双向扩展 JavaScript 方法 **getSchemas** 和 **getStatus**填充的双向响应集。

<a name="members"></a>成员
-------

**IPrinterBidiSchemaResponses**接口继承自[**IUnknown**](/windows/win32/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterBidiSchemaResponses** 还具有下列类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterBidiSchemaResponses**接口具有这些方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="iprinterbidischemaresponses--addbool.md" data-raw-source="[&lt;strong&gt;AddBool&lt;/strong&gt;](iprinterbidischemaresponses--addbool.md)"><strong>AddBool</strong></a></td>
<td><p>AddBool 方法将 BIDI_BOOL 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses--addint32.md" data-raw-source="[&lt;strong&gt;AddInt32&lt;/strong&gt;](iprinterbidischemaresponses--addint32.md)"><strong>AddInt32</strong></a></td>
<td><p>AddInt32 方法将 BIDI_INT 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addblob.md" data-raw-source="[&lt;strong&gt;AddBlob&lt;/strong&gt;](iprinterbidischemaresponses-addblob.md)"><strong>AddBlob</strong></a></td>
<td><p>AddBlob 方法将 BIDI_BLOB 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addenum.md" data-raw-source="[&lt;strong&gt;AddEnum&lt;/strong&gt;](iprinterbidischemaresponses-addenum.md)"><strong>AddEnum</strong></a></td>
<td><p>AddEnum 方法将 BIDI_ENUM 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addfloat.md" data-raw-source="[&lt;strong&gt;AddFloat&lt;/strong&gt;](iprinterbidischemaresponses-addfloat.md)"><strong>AddFloat</strong></a></td>
<td><p>AddFloat 方法将 BIDI_FLOAT 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addnull.md" data-raw-source="[&lt;strong&gt;AddNull&lt;/strong&gt;](iprinterbidischemaresponses-addnull.md)"><strong>AddNull</strong></a></td>
<td><p>AddNull 方法将 BIDI_NULL 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addrequerykey.md" data-raw-source="[&lt;strong&gt;AddRequeryKey&lt;/strong&gt;](iprinterbidischemaresponses-addrequerykey.md)"><strong>AddRequeryKey</strong></a></td>
<td><p>AddRequeryKey 方法添加新的查询密钥，以在从 getSchemas 调用返回时重新查询。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addstring.md" data-raw-source="[&lt;strong&gt;AddString&lt;/strong&gt;](iprinterbidischemaresponses-addstring.md)"><strong>AddString</strong></a></td>
<td><p>AddString 方法将 BIDI_STRING 类型的新响应添加到集合中。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addtext.md" data-raw-source="[&lt;strong&gt;AddText&lt;/strong&gt;](iprinterbidischemaresponses-addtext.md)"><strong>AddText</strong></a></td>
<td><p>Shapes.addtext 方法将 BIDI_TEXT 类型的新响应添加到集合中。</p></td>
</tr>
</tbody>
</table>