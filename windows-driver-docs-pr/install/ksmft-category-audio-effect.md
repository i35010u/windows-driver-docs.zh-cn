---
title: KSMFT_CATEGORY_AUDIO_EFFECT
description: KSMFT_CATEGORY_AUDIO_EFFECT
ms.assetid: a6747c99-3c16-4833-905a-52472a854f77
keywords:
- KSMFT_CATEGORY_AUDIO_EFFECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_AUDIO_EFFECT
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dde4bcbbb5bcd65dfdfb16d6ebe014d1bc415ec9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386035"
---
# <a name="ksmftcategoryaudioeffect"></a>KSMFT_CATEGORY_AUDIO_EFFECT


KSMFT_CATEGORY_AUDIO_EFFECT[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)(KS) 音频设备的功能类别。

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
<td align="left"><p>KSMFT_CATEGORY_AUDIO_EFFECT</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{11064c48-3648-4ed0-932e-05ce8ac811b7}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

AVStream 驱动程序 MFT 编解码器支持注册此设备接口类，以向操作系统指示设备支持 KSMFT_CATEGORY_AUDIO_EFFECT 功能分类的实例。

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

 

 





