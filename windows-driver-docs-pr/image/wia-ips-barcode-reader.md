---
title: WIA \_ IP \_ 条形码 \_ 读取器
description: '\_ \_ Wia 微型驱动程序使用 "wia ip 条形码 \_ 读取器" 属性来列出可用的条形码读取器位置 (一/固定或多个) ，并由应用程序客户端用于选择其中一个位置并启用条形码检测。'
keywords:
- WIA_IPS_BARCODE_READER 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d51e32e716b85416d505e81afe92bf0167ecb84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839911"
---
# <a name="wia_ips_barcode_reader"></a>WIA \_ IP \_ 条形码 \_ 读取器


WIA 微型驱动程序使用 " **wia \_ ip \_ 条形码 \_ 读取器** " 属性来列出可用的条形码读取器位置 (一/固定或多个) ，并由应用程序客户端用于选择其中一个位置并启用条形码检测。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ ip \_ 条形码 \_ 读取器** " 属性的必需值。

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
<td><p>WIA_BARCODE_READER_DISABLED</p></td>
<td><p>禁用条形码检测。 这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_AUTO</p></td>
<td><p>启用条形码检测。 设备会在运行时根据活动扫描输入源自动选择条形码读取器位置。</p></td>
</tr>
</tbody>
</table>

 

下表描述了 " **WIA \_ ip \_ 条形码 \_ 读取器** " 属性的可选值。

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
<td><p>WIA_BARCODE_READER_FLATBED</p></td>
<td><p>为扫描程序平板扫描的文档启用了条形码检测。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_FEEDER_FRONT</p></td>
<td><p>在扫描仪进纸器上扫描的文档的正面启用条形码检测。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_READER_FEEDER_BACK</p></td>
<td><p>在扫描仪进纸器上扫描的文档的正面启用条形码检测。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_FEEDER_DUPLEX</p></td>
<td><p>启用条形码检测。 设备会在运行时根据活动扫描输入源自动选择条形码读取器位置。</p></td>
</tr>
</tbody>
</table>

 

**注意**  允许 WIA 微型驱动程序接受可选值的属性配置，但在扫描时忽略请求以启用对非活动扫描输入源的条码检测。

 

所有条形码读取器项都需要此属性。 禁用了 WIA \_ 条形码 \_ 读取器 \_ 和 wia \_ 条形码 \_ 读取器 \_ 自动值。 \_禁用 WIA 条形码 \_ 读取器 \_ 是必需的默认值。

所有条形码读取器项还需要 [**WIA \_ IPA \_ 格式**](wia-ipa-format.md) 属性。

下表描述了在条形码读取器项上实现时， [**WIA \_ IPA \_ FORMAT**](wia-ipa-format.md) 属性所需的值。

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
<td><p>WiaImgFmt_XmlBar</p></td>
<td><p>将条码元数据作为其内容符合 WIA 条码元数据架构的 XML 文件传输。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawBar</p></td>
<td><p>将条码元数据作为 WIA 条码元数据原始格式文件传输。</p></td>
</tr>
</tbody>
</table>

 

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

 

 





