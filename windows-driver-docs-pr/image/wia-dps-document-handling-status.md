---
title: WIA\_DPS\_文档\_处理\_状态
description: WIA\_DPS\_文档\_处理\_STATUS 属性包含的扫描程序的已安装的平板、 文档送纸器或双面打印器的当前状态。
ms.assetid: b95c64ee-b06c-4786-87d3-d8a0f91dcba2
keywords:
- WIA_DPS_DOCUMENT_HANDLING_STATUS 成像设备
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
ms.openlocfilehash: 7ca93425375b610ad3eaa5c77da7916b4df5e20b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373931"
---
# <a name="wiadpsdocumenthandlingstatus"></a>WIA\_DPS\_文档\_处理\_状态


WIA\_DPS\_文档\_处理\_STATUS 属性包含的扫描程序的已安装的平板、 文档送纸器或双面打印器的当前状态。

## <span id="ddk_wia_dps_document_handling_status_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_STATUS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_文档\_处理\_STATUS 属性以确定是否已准备好使用扫描程序设备。 读取此属性是检查纸张是否在送纸器之前用户获取图像的理想方法。 WIA 微型驱动程序创建并维护此属性。

下表描述了与 Windows 8 和更高版本 Windows 的有效的常量。

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
<td><p>IMPRINTER_READY</p></td>
<td><p>印刷器/印记签署器的印刷器功能是已启用并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>ENDORSER_READY</p></td>
<td><p>印刷器/印记签署器的印记签署器功能是已启用并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>BARCODE_READER_READY</p></td>
<td><p>条码读取器已启用并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>PATCH_CODE_READER_READY</p></td>
<td><p>修补程序代码读取器是已启用并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>MICR_READER_READY</p></td>
<td><p>MICR 读取器是已启用并可供使用。</p></td>
</tr>
</tbody>
</table>

 

下表描述了与 Windows Vista 和 Windows XP 有效的常量。

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
<td><p>双面打印器已启用并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>FEED_READY</p></td>
<td><p>文档送纸器已加载的页面，并随时可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>FLAT_COVER_UP</p></td>
<td><p>平台封面已启动。</p></td>
</tr>
<tr class="even">
<td><p>FLAT_READY</p></td>
<td><p>平板便可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>PAPER_JAM</p></td>
<td><p>文档卡在文档送纸器中。</p></td>
</tr>
<tr class="even">
<td><p>PATH_COVER_UP</p></td>
<td><p>纸张路径包含且，导致无法正确操作。</p></td>
</tr>
</tbody>
</table>

 

下表介绍才有效，且 Windows Vista 的常量。

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
<td><p>透明度适配器是一个已安装并可供使用。</p></td>
</tr>
<tr class="even">
<td><p>STORAGE_READY</p></td>
<td><p>存储设备是已安装并可供使用。</p></td>
</tr>
<tr class="odd">
<td><p>STORAGE_FULL</p></td>
<td><p>存储已满;没有上传操作可能会出现。</p></td>
</tr>
<tr class="even">
<td><p>MULTIPLE_FEED</p></td>
<td><p>多个源出现则PAPER_JAM 值，通常会出现这种类型的源。</p></td>
</tr>
<tr class="odd">
<td><p>DEVICE_ATTENTION</p></td>
<td><p>没有需要用户干预的扫描错误。</p></td>
</tr>
<tr class="even">
<td><p>LAMP_ERR</p></td>
<td><p>扫描程序具有 lamp 问题并且不准备就绪。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  没有任何自定义的基本定义。 无法创建自定义扩展状态的标志值。 如果需要自定义状态报告，则应定义自定义属性。

 

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

 

 





