---
title: WIA \_ IP \_ 磁墨 \_ 读取器
description: WIA 微型驱动程序使用 "WIA \_ ip \_ 磁墨识别 \_ 器" 属性来报告磁墨字符识别 (磁墨) 读卡器可用的位置。 WIA 客户端应用程序可以选择在其中启用磁墨检测的这些位置之一。
keywords:
- WIA_IPS_MICR_READER 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MICR_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d34f488304bd89c335b64b4d51023a0a873fea9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792229"
---
# <a name="wia_ips_micr_reader"></a>WIA \_ IP \_ 磁墨 \_ 读取器


WIA 微型驱动程序使用 " **wia \_ ip \_ 磁墨识别 \_ 器** " 属性来报告磁墨字符识别 (磁墨) 读卡器可用的位置。 WIA 客户端应用程序可以选择在其中启用磁墨检测的这些位置之一。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 **WIA \_ ip \_ 磁墨识别 \_ 器** 属性的必需值。

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
<td><p>WIA_MICR_READER_DISABLED</p></td>
<td><p>已禁用磁墨检测。 这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_AUTO</p></td>
<td><p>已启用磁墨检测。 磁墨字符识别器的位置是固定的，或在运行时设备根据活动扫描输入源自动选择。</p></td>
</tr>
</tbody>
</table>

 

所有磁墨磁墨读者项都需要此属性。 禁用了 WIA \_ 磁墨 \_ 读取器 \_ ，并 \_ 需要 wia \_ \_ 记忆器自动值。 WIA \_ 磁墨 \_ 读取器 \_ 禁用是所需的默认值。

下表描述了 " **WIA \_ ip \_ 磁墨识别 \_ 器** " 属性的可选值。

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
<td><p>WIA_MICR_READER_FLATBED</p></td>
<td><p>磁墨磁墨检测功能已对平板扫描的文档启用。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_FEEDER_FRONT</p></td>
<td><p>为通过送纸器扫描的文档的正面启用磁墨检测。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MICR_READER_FEEDER_BACK</p></td>
<td><p>为通过送纸器扫描的文档的正面启用磁墨检测。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_FEEDER_DUPLEX</p></td>
<td><p>磁墨磁墨检测已为通过送纸器扫描的文档的正面和背面启用。</p></td>
</tr>
</tbody>
</table>

 

**注意**  允许 WIA 微型驱动程序接受可选值的属性配置，但在扫描时忽略请求，以启用磁墨扫描输入源的不活动扫描。

 

所有磁墨字符识别器项还需要 [**WIA \_ IPA \_ 格式**](wia-ipa-format.md) 属性。

下表描述了在磁墨磁墨读取器项上实现时， [**WIA \_ IPA \_ FORMAT**](wia-ipa-format.md) 属性所需的值。

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
<td><p>WiaImgFmt_XmlMic</p></td>
<td><p>磁墨识别元数据将作为其内容符合 WIA 磁墨的元数据架构的 XML 文件传输。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawMic</p></td>
<td><p>磁墨识别元数据将作为 WIA 磁墨元数据原始格式文件传输。</p></td>
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

 

 





