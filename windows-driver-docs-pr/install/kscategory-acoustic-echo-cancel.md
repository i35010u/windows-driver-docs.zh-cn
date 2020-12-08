---
title: KSCATEGORY_ACOUSTIC_ECHO_CANCEL
description: KSCATEGORY_ACOUSTIC_ECHO_CANCEL
keywords:
- KSCATEGORY_ACOUSTIC_ECHO_CANCEL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_ACOUSTIC_ECHO_CANCEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6643cf2da5def2f7583862b3a2e4188968c71cc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820135"
---
# <a name="kscategory_acoustic_echo_cancel"></a>KSCATEGORY_ACOUSTIC_ECHO_CANCEL


KSCATEGORY_ACOUSTIC_ECHO_CANCEL [设备接口类](./overview-of-device-interface-classes.md) 是针对 [核心流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的，用于执行声音回声取消。

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
<td align="left"><p>KSCATEGORY_ACOUSTIC_ECHO_CANCEL</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{BF963D80-C559-11D0-8A2B-00A0C9255AC1}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 KS 音频设备的驱动程序将 KSCATEGORY_ACOUSTIC_ECHO_CANCEL 的实例注册，以向操作系统指示设备是否支持用于执行声音回声取消的 KS 功能类别。

有关音频适配器的设备接口类的信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)。

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

 

