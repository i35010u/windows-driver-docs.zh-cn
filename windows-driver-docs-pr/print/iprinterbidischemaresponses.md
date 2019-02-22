---
title: IPrinterBidiSchemaResponses 接口
description: IPrinterBidiSchemaResponses 接口表示一的系列由 USB Bidi 扩展 JavaScript 方法 getSchemas 和 getStatus 填充 bidi 响应。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 2E68C4AA-D235-46D2-81D6-D6C7E84C2FEF
keywords:
- IPrinterBidiSchemaResponses 接口打印设备
- IPrinterBidiSchemaResponses 接口所述的打印设备
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd0284b80dbeeaf157c5686fb72ba242d816bb1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554744"
---
# <a name="iprinterbidischemaresponses-interface"></a>IPrinterBidiSchemaResponses 接口

IPrinterBidiSchemaResponses 接口表示的一系列由 USB Bidi 扩展 JavaScript 方法填充 bidi 响应**getSchemas**并**getStatus**。

<a name="members"></a>成员
-------

**IPrinterBidiSchemaResponses**接口继承自[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)接口。 **IPrinterBidiSchemaResponses**还具有这些类型的成员：

-   [方法](#methods)

### <a name="methods"></a>方法

**IPrinterBidiSchemaResponses**接口提供以下方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="iprinterbidischemaresponses--addbool.md" data-raw-source="[&lt;strong&gt;AddBool&lt;/strong&gt;](iprinterbidischemaresponses--addbool.md)"><strong>AddBool</strong></a></td>
<td><p>AddBool 方法向集合添加类型 BIDI_BOOL 的新响应。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses--addint32.md" data-raw-source="[&lt;strong&gt;AddInt32&lt;/strong&gt;](iprinterbidischemaresponses--addint32.md)"><strong>AddInt32</strong></a></td>
<td><p>AddInt32 方法向集合添加类型 BIDI_INT 的新响应。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addblob.md" data-raw-source="[&lt;strong&gt;AddBlob&lt;/strong&gt;](iprinterbidischemaresponses-addblob.md)"><strong>AddBlob</strong></a></td>
<td><p>AddBlob 方法向集合添加类型 BIDI_BLOB 的新响应。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addenum.md" data-raw-source="[&lt;strong&gt;AddEnum&lt;/strong&gt;](iprinterbidischemaresponses-addenum.md)"><strong>AddEnum</strong></a></td>
<td><p>AddEnum 方法向集合添加类型 BIDI_ENUM 的新响应。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addfloat.md" data-raw-source="[&lt;strong&gt;AddFloat&lt;/strong&gt;](iprinterbidischemaresponses-addfloat.md)"><strong>AddFloat</strong></a></td>
<td><p>AddFloat 方法向集合添加类型 BIDI_FLOAT 的新响应。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addnull.md" data-raw-source="[&lt;strong&gt;AddNull&lt;/strong&gt;](iprinterbidischemaresponses-addnull.md)"><strong>AddNull</strong></a></td>
<td><p>AddNull 方法向集合添加类型 BIDI_NULL 的新响应。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addrequerykey.md" data-raw-source="[&lt;strong&gt;AddRequeryKey&lt;/strong&gt;](iprinterbidischemaresponses-addrequerykey.md)"><strong>AddRequeryKey</strong></a></td>
<td><p>AddRequeryKey 方法将添加新的查询密钥，以重新查询从 getSchemas 调用返回时。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterbidischemaresponses-addstring.md" data-raw-source="[&lt;strong&gt;AddString&lt;/strong&gt;](iprinterbidischemaresponses-addstring.md)"><strong>AddString</strong></a></td>
<td><p>AddString 方法向集合添加类型 BIDI_STRING 的新响应。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterbidischemaresponses-addtext.md" data-raw-source="[&lt;strong&gt;AddText&lt;/strong&gt;](iprinterbidischemaresponses-addtext.md)"><strong>AddText</strong></a></td>
<td><p>AddText 方法向集合添加类型 BIDI_TEXT 的新响应。</p></td>
</tr>
</tbody>
</table>
