---
title: KSMFT_CATEGORY_VIDEO_DECODER
description: KSMFT_CATEGORY_VIDEO_DECODER
ms.assetid: 56f2c39a-dea6-4dc0-84bb-f052d27fb084
keywords:
- KSMFT_CATEGORY_VIDEO_DECODER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_VIDEO_DECODER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ab02b3c98d6c74563e8c7108593d2bbbdcb85124
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386026"
---
# <a name="ksmftcategoryvideodecoder"></a>KSMFT_CATEGORY_VIDEO_DECODER


KSMFT_CATEGORY_VIDEO_DECODER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)视频设备 (KS) 功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSMFT_CATEGORY_VIDEO_DECODER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{d6c02d4b-6833-45b4-971a-05a4b04bab91}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

AVStream 驱动程序 MFT 编解码器支持注册此设备接口类，以向操作系统指示设备支持 KSMFT_CATEGORY_VIDEO_DECODER 功能分类的实例。

有关 AVStream 编解码器支持硬件设备的设备接口类的详细信息，请参阅[开始使用硬件 AVStream 中支持的编解码器](https://docs.microsoft.com/windows-hardware/drivers/stream/getting-started-with-hardware-codec-support-in-avstream)。

有关如何在一个 INF 文件中注册此功能的类别的详细信息，请参阅*Hiddigi.inf*文件，它是随*src\\输入\\hiddigi*示例WDK 中的驱动程序。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

 

 





