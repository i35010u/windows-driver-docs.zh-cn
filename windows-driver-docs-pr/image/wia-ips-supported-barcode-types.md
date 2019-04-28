---
title: WIA\_IPS\_支持\_条形码\_类型
description: WIA\_IPS\_支持\_条形码\_WIA 微型驱动程序支持所有的条形码类型 （理解） 的条形码读取器的列表到使用类型属性。
ms.assetid: 38CA1167-25DB-4495-B31A-F996671E2686
keywords:
- WIA_IPS_SUPPORTED_BARCODE_TYPES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SUPPORTED_BARCODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c454e2deea3ad0f27476f75fff549f8541f59cd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343837"
---
# <a name="wiaipssupportedbarcodetypes"></a>WIA\_IPS\_支持\_条形码\_类型


**WIA\_IPS\_支持\_条形码\_类型**属性由 WIA 微型驱动程序支持所有的条形码类型 （理解） 的条形码读取器的列表。 受支持的条形码类型报告中 VT\_向量数组作为单个值，该值包含多个条目。




属性类型：VT\_I4 | VT\_VECTOR

有效值：WIA\_PROP\_NONE （单个数组/向量值）

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_支持\_条形码\_类型**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BARCODE_UPCA</p></td>
<td><p>通用产品代码 UPC A</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_UPCE</p></td>
<td><p>通用产品代码 UPC-E</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODABAR</p></td>
<td><p>Codabar 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_NONINTERLEAVED_2OF5</p></td>
<td><p>两个扩展的五代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_INTERLEAVED_2OF5</p></td>
<td><p>已交错的 2 的 5 个代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE39</p></td>
<td><p>Code 39</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE39_MOD43</p></td>
<td><p>代码 39 mod 43</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE39_FULLASCII</p></td>
<td><p>完整的 ASCII 代码 39</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE93</p></td>
<td><p>代码 93</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE128</p></td>
<td><p>Code 128</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE128A</p></td>
<td><p>代码 128A</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE128B</p></td>
<td><p>代码 128B</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE128C</p></td>
<td><p>代码 128 C</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_GS1128</p></td>
<td><p>GS1-128 （以前称为 UCC/EAN-128）</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_GS1DATABAR WIA_BARCODE_ITF14</p></td>
<td><p>GS1 数据条代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_ITF14</p></td>
<td><p>接口 14 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_EAN8</p></td>
<td><p>EAN 8 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_EAN13</p></td>
<td><p>EAN 13 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTNETA</p></td>
<td><p>POSTNET （邮政数字编码技术）"A"代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_POSTNETB</p></td>
<td><p>POSTNET （邮政数字编码技术）"B"代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTNETC</p></td>
<td><p>POSTNET （邮政数字编码技术）"C"代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_POSTNET_DPBC</p></td>
<td><p>POSTNET （邮政数字编码技术） DPBC （交付点兵絏） 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PLANET</p></td>
<td><p>邮政编码 Alpha 数字编码技术 （全球）</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_INTELLIGENT_MAIL</p></td>
<td><p>智能邮件条形码 （替换 POSTNET 和全球条形码）</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTBAR</p></td>
<td><p>PostBar （也称为 cpc 解决 4-状态）</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_RM4SCC</p></td>
<td><p>RM4SCC 条形码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_HIGH_CAPACITY_COLOR</p></td>
<td><p>Microsoft 高容量彩色条形码 (HCCB)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_MAXICODE</p></td>
<td><p>MaxiCode</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PDF417</p></td>
<td><p>PDF417</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CPCBINARY</p></td>
<td><p>Cpc 解决二进制条形码 （加拿大文章）</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_FIM</p></td>
<td><p>人脸 Id 标记 (FIM) 条形码 (USPS)</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_PHARMACODE</p></td>
<td><p>医药二进制代码 (Pharmacode)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PLESSEY</p></td>
<td><p>Plessey 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_MSI</p></td>
<td><p>MSI (修改 Plessey) 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_JAN</p></td>
<td><p>日语文章编号 (JAN) 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_TELEPEN</p></td>
<td><p>Telepen 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_AZTEC</p></td>
<td><p>Aztec Code</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_SMALLAZTEC</p></td>
<td><p>小型 Aztec 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_DATAMATRIX</p></td>
<td><p>数据矩阵代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_DATASTRIP</p></td>
<td><p>Datastrip 代码 (Cauzin Softstrip)</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_EZCODE</p></td>
<td><p>Ezcode</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_QRCODE</p></td>
<td><p>QR 码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_SHOTCODE</p></td>
<td><p>ShotCode</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_SPARQCODE</p></td>
<td><p>SPARQCode</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CUSTOM_BASE + N</p></td>
<td><p>WIA_BARCODE_CUSTOM_BASE 是到 WIA 微型驱动程序可能添加的所有自定义的条形码值的偏移量。 N 是一个正整数。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序可以使用定义为 WIA 的其他自定义值来扩展此列表\_条形码\_自定义\_基本 + N，其中 N 是一个正整数。

此属性是必需的所有条码读取器项。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





