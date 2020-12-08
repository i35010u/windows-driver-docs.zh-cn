---
title: KSCATEGORY_SYNTHESIZER
description: KSCATEGORY_SYNTHESIZER
keywords:
- KSCATEGORY_SYNTHESIZER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_SYNTHESIZER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 280080fcbb7ad9c7187b99f389d6a1e28b5f7c0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787401"
---
# <a name="kscategory_synthesizer"></a>KSCATEGORY_SYNTHESIZER


KSCATEGORY_SYNTHESIZER [设备接口类](./overview-of-device-interface-classes.md) 定义为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别，该类别将 MIDI 数据转换为波形音频样本或模拟输出信号。

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
<td align="left"><p>KSCATEGORY_SYNTHESIZER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{DFF220F3-F70F-11D0-B917-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 KS 音频适配器设备的驱动程序将 KSCATEGORY_SYNTHESIZER 的实例注册，以指示操作系统设备支持 KSCATEGORY_SYNTHESIZER 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的 *src \\ 音频 \\ Ddksynth* 目录中的软件合成器示例附带的 *Ddksynth* inf 文件。

有关合成器的一般信息，请参阅 [MIDI 和 DirectMusic 筛选器](../audio/midi-and-directmusic-filters.md)。

有关音频适配器的设备接口类的常规信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

