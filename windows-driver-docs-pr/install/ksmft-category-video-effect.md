---
title: KSMFT_CATEGORY_VIDEO_EFFECT
description: KSMFT_CATEGORY_VIDEO_EFFECT
ms.assetid: 81286240-d6eb-4872-a06c-34046767a2cc
keywords:
- KSMFT_CATEGORY_VIDEO_EFFECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_VIDEO_EFFECT
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3089d197622b83a0ce8b7998ec724c6500c565a7
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095031"
---
# <a name="ksmft_category_video_effect"></a>KSMFT_CATEGORY_VIDEO_EFFECT


为视频设备的[内核流式处理](../stream/kernel-streaming.md) (KS) 功能类别定义 KSMFT_CATEGORY_VIDEO_EFFECT[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSMFT_CATEGORY_VIDEO_EFFECT</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{12e17c21-532c-4a6e-8a1c-40825a736397}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

具有 MFT 编解码器的 AVStream 驱动程序支持注册此设备接口类的实例，以指示操作系统设备支持 KSMFT_CATEGORY_VIDEO_EFFECT 功能类别。

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

 

