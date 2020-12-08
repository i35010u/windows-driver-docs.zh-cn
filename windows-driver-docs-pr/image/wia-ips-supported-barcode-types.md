---
title: WIA \_ IPS \_ 支持的 \_ 条形码 \_ 类型
description: '\_ \_ Wia 微型驱动程序使用 "wia IPS 支持的 \_ 条形码类型" \_ 属性来列出条形码读取器 () 理解的所有支持的条形码类型。'
keywords:
- WIA_IPS_SUPPORTED_BARCODE_TYPES 图像设备
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
ms.openlocfilehash: bfa44e510f11ddc1c1b9eb045167046c421c4655
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841257"
---
# <a name="wia_ips_supported_barcode_types"></a>WIA \_ IPS \_ 支持的 \_ 条形码 \_ 类型


WIA 微型驱动程序使用 " **wia \_ IPS \_ 支持的 \_ 条形码 \_ 类型** " 属性来列出条形码读取器 () 理解的所有支持的条形码类型。 支持的条码类型在 VT \_ 矢量数组中报告为包含多个条目的单个值。




属性类型： VT \_ I4 |VT \_ 矢量

有效值： WIA \_ \_ NONE (单个数组/向量值) 

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ IPS \_ 支持的 \_ 条形码 \_ 类型** " 属性的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BARCODE_UPCA</p></td>
<td><p>通用产品代码 UPC-A</p></td>
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
<td><p>两个-五个代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_INTERLEAVED_2OF5</p></td>
<td><p>交错2个（共5个）代码</p></td>
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
<td><p>完整的 ASCII 代码39</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE93</p></td>
<td><p>代码93</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE128</p></td>
<td><p>Code 128</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE128A</p></td>
<td><p>代码128A</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_CODE128B</p></td>
<td><p>代码128B</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_CODE128C</p></td>
<td><p>代码128C</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_GS1128</p></td>
<td><p>GS1-128 (以前称为 UCC/EAN-128) </p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_GS1DATABAR WIA_BARCODE_ITF14</p></td>
<td><p>GS1 数据条形代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_ITF14</p></td>
<td><p>ITF-14 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_EAN8</p></td>
<td><p>EAN-8 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_EAN13</p></td>
<td><p>EAN-13 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTNETA</p></td>
<td><p>POSTNET (邮政数字编码方法) "A" 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_POSTNETB</p></td>
<td><p>POSTNET (邮政编码) "B" 代码的数字编码方法</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTNETC</p></td>
<td><p>POSTNET (邮政数字编码技术) "C" 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_POSTNET_DPBC</p></td>
<td><p>POSTNET (邮政数字编码方法) DPBC (传递点条码) 代码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PLANET</p></td>
<td><p>邮政 Alpha 编码方法 (行星) 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_INTELLIGENT_MAIL</p></td>
<td><p>智能邮件条形码 (替换 POSTNET 和行星) </p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_POSTBAR</p></td>
<td><p>PostBar (也称为 CPC 4-State) </p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_RM4SCC</p></td>
<td><p>RM4SCC 条形码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_HIGH_CAPACITY_COLOR</p></td>
<td><p>Microsoft 高容量彩色条形码 (HCCB) </p></td>
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
<td><p> (加拿大发布) 的 CPC 二进制条形码</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_FIM</p></td>
<td><p>面部标识标记 (FIM) 条形码 (USPS) </p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_PHARMACODE</p></td>
<td><p>药物二进制代码 (Pharmacode) </p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_PLESSEY</p></td>
<td><p>Plessey 代码</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_MSI</p></td>
<td><p>MSI (修改后的 Plessey) 代码</p></td>
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
<td><p>Aztec 代码</p></td>
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
<td><p>Datastrip code (Cauzin Softstrip) </p></td>
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
<td><p>WIA_BARCODE_CUSTOM_BASE 是 WIA 微型驱动程序可以添加的所有自定义条码值的偏移量。 N 是一个正整数。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序可以扩展此列表，并将其他自定义值定义为 WIA \_ 条形码 \_ 自定义 \_ 基数 + N，其中 N 是一个正整数。

所有条形码读取器项都需要此属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





