---
title: KSMFT_CATEGORY_VIDEO_PROCESSOR
description: KSMFT_CATEGORY_VIDEO_PROCESSOR
ms.assetid: 9d27cea3-0d4f-4812-9e87-0b2295c99a5f
keywords:
- KSMFT_CATEGORY_VIDEO_PROCESSOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_VIDEO_PROCESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3cd8e03d971c161779a7efe710e1fac7eb9be693
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095027"
---
# <a name="ksmft_category_video_processor"></a>KSMFT_CATEGORY_VIDEO_PROCESSOR


为视频设备的[内核流式处理](../stream/kernel-streaming.md) (KS) 功能类别定义 KSMFT_CATEGORY_VIDEO_PROCESSOR[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSMFT_CATEGORY_VIDEO_PROCESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{302ea3fc-aa5f-47f9-9f7a-c2188bb16302}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

具有 MFT 编解码器的 AVStream 驱动程序支持注册此设备接口类的实例，以指示操作系统设备支持 KSMFT_CATEGORY_VIDEO_PROCESSOR 功能类别。

有关硬件编解码器支持的 AVStream 设备的设备接口类的详细信息，请参阅 [AVStream 中具有硬件编解码器支持的入门](../stream/getting-started-with-hardware-codec-support-in-avstream.md)。

有关如何在 INF 文件中注册此功能类别的详细信息，请参阅 *Hiddigi* 文件，该文件包含在 WDK 的 *src \\ 输入 \\ Hiddigi* 示例驱动程序中。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

 

