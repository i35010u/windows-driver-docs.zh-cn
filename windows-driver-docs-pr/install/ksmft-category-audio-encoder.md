---
title: KSMFT_CATEGORY_AUDIO_ENCODER
description: KSMFT_CATEGORY_AUDIO_ENCODER
ms.assetid: b8be392e-6211-46ba-8b99-edcccb7ef8fb
keywords:
- KSMFT_CATEGORY_AUDIO_ENCODER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_AUDIO_ENCODER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 39079a722c794d5d0f7a9c3fbe0167a0996f4a41
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097335"
---
# <a name="ksmft_category_audio_encoder"></a>KSMFT_CATEGORY_AUDIO_ENCODER


为音频设备的[内核流式处理](../stream/kernel-streaming.md) (KS) 功能类别定义 KSMFT_CATEGORY_AUDIO_ENCODER[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSMFT_CATEGORY_AUDIO_ENCODER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{91c64bd0-f91e-4d8c-9276-db248279d975}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

具有 MFT 编解码器的 AVStream 驱动程序支持注册此设备接口类的实例，以指示操作系统设备支持 KSMFT_CATEGORY_AUDIO_ENCODER 功能类别。

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

 

