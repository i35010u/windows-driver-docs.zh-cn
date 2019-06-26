---
title: KSCATEGORY_REALTIME
description: KSCATEGORY_REALTIME
ms.assetid: c9b0a31a-50d9-47bc-9345-5d73a95238c3
keywords:
- KSCATEGORY_REALTIME 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_REALTIME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5fb1944316e280f67c50f264591370b0148e335f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355144"
---
# <a name="kscategoryrealtime"></a>KSCATEGORY_REALTIME


KSCATEGORY_REALTIME[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 连接到系统总线 （例如，PCI 总线），将音频设备的功能类别播放或捕获实时波形数据。

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
<td align="left"><p>KSCATEGORY_REALTIME</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{EB115FFC-10C8-4964-831D-6DCB02E6F23F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_REALTIME 向操作系统指示设备支持 KSCATEGORY_REALTIME 功能分类的实例。

注册此功能的类别的设备由系统提供运营[WaveRT 端口驱动程序](https://docs.microsoft.com/previous-versions/ff538837(v=vs.85))。

有关如何在一个 INF 文件中注册此功能的类别的信息，请参阅 INF 文件*Ac97smpl.inf*随[AC'97 示例驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256075)WDK 中。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





