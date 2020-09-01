---
title: KSCATEGORY_CROSSBAR
description: KSCATEGORY_CROSSBAR
ms.assetid: 0a5edfd5-ad50-4402-8f6d-d6c5018d1ab2
keywords:
- KSCATEGORY_CROSSBAR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_CROSSBAR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26c15c1633e97abd469b45467e3d0e3ca40a1d01
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097255"
---
# <a name="kscategory_crossbar"></a>KSCATEGORY_CROSSBAR


为传输视频和音频流的纵横比设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_CROSSBAR[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_CROSSBAR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A799A801-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_CROSSBAR 的实例，以向操作系统指示设备支持 KSCATEGORY_CROSSBAR 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的*src \\ swtuner \\ algtuner*目录中的软件调谐器示例附带的*Bdan* inf 文件。

有关音频和视频的纵横比设备的信息，请参阅 [视频捕获设备](../stream/filters-used-with-the-video-capture-devices.md) 和 [模拟视频类别](../stream/analog-video-category.md)中使用的筛选器。

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

 

