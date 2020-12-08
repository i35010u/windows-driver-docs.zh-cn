---
title: KSCATEGORY_REALTIME
description: KSCATEGORY_REALTIME
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
ms.openlocfilehash: a3920fbddce7ee04b41c25000aec0adaf72000b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787419"
---
# <a name="kscategory_realtime"></a>KSCATEGORY_REALTIME


KSCATEGORY_REALTIME [设备接口类](./overview-of-device-interface-classes.md) 是为连接到系统总线的音频设备的 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的 (例如，PCI 总线) 并可实时捕获波数据。

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

KS 设备的驱动程序将注册 KSCATEGORY_REALTIME 的实例，以向操作系统指示设备支持 KSCATEGORY_REALTIME 功能类别。

注册此功能类别的设备由系统提供的 [WaveRT 端口驱动程序](/previous-versions/ff538837(v=vs.85))运行。

有关如何在 INF 文件中注册此功能类别的信息，请参阅在 WDK 中随附 [AC ' 97 示例驱动程序](/samples/browse/)的 Inf 文件 *Ac97smpl。*

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

