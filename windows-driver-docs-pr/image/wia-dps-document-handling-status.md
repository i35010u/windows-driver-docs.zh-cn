---
title: WIA \_ DPS \_ 文档 \_ 处理 \_ 状态
description: WIA \_ DPS \_ 文档 \_ 处理 \_ 状态属性包含扫描仪安装的平板、文档送纸器或双面打印器的当前状态。
keywords:
- WIA_DPS_DOCUMENT_HANDLING_STATUS 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f51238ca40de08f081381b1fdf59c6db6194784e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836995"
---
# <a name="wia_dps_document_handling_status"></a>WIA \_ DPS \_ 文档 \_ 处理 \_ 状态


WIA \_ DPS \_ 文档 \_ 处理 \_ 状态属性包含扫描仪安装的平板、文档送纸器或双面打印器的当前状态。

## <span id="ddk_wia_dps_document_handling_status_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_STATUS_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA \_ DPS \_ 文档 \_ 处理 \_ 状态属性，以确定扫描仪设备是否可供使用。 读取此属性是在用户获取图像之前检查纸张是否位于送纸器中的理想方法。 WIA 微型驱动程序创建并维护此属性。

下表介绍了在 Windows 8 和更高版本的 Windows 中有效的常量。

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
<td><p>IMPRINTER_READY</p></td>
<td><p>Imprinter/endorser 的 imprinter 功能已启用并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>ENDORSER_READY</p></td>
<td><p>Imprinter/endorser 的 endorser 功能已启用并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>BARCODE_READER_READY</p></td>
<td><p>条形码读取器已启用并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>PATCH_CODE_READER_READY</p></td>
<td><p>修补程序代码读取器已启用并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>MICR_READER_READY</p></td>
<td><p>磁墨磁墨读取器已启用并可供使用。</p></td>
</tr>
</tbody>
</table>

 

下表描述了对 Windows Vista 和 Windows XP 均有效的常量。

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
<td><p>DUP_READY</p></td>
<td><p>已启用双面打印器并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>FEED_READY</p></td>
<td><p>文档送纸器已加载页面并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>FLAT_COVER_UP</p></td>
<td><p>平板覆盖处于启动状态。</p></td>
</tr>
<tr class="even">
<td><p>FLAT_READY</p></td>
<td><p>平台已准备就绪，可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>PAPER_JAM</p></td>
<td><p>文档卡在文档送纸器中。</p></td>
</tr>
<tr class="even">
<td><p>PATH_COVER_UP</p></td>
<td><p>纸张路径已涵盖，并阻止操作正常。</p></td>
</tr>
</tbody>
</table>

 

下表描述了仅适用于 Windows Vista 的常量。

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
<td><p>FILM_TPA_READY</p></td>
<td><p>透明度适配器已安装并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>STORAGE_READY</p></td>
<td><p>存储设备已安装并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>STORAGE_FULL</p></td>
<td><p>存储已满;不能进行上传操作。</p></td>
</tr>
<tr class="even">
<td><p>MULTIPLE_FEED</p></td>
<td><p>发生了多个源;这种类型的源通常会出现 PAPER_JAM 值。</p></td>
</tr>
<tr class="odd">
<td><p>DEVICE_ATTENTION</p></td>
<td><p>出现错误，要求用户在扫描仪上介入。</p></td>
</tr>
<tr class="even">
<td><p>LAMP_ERR</p></td>
<td><p>扫描仪出现灯泡问题，未就绪。</p></td>
</tr>
</tbody>
</table>

 

**注意**   没有自定义的基定义。 不能为状态标志值创建自定义扩展。 如果需要自定义状态报告，则应定义自定义属性。

 

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

 

 





