---
title: KSCATEGORY_DRM_DESCRAMBLE
description: KSCATEGORY_DRM_DESCRAMBLE
ms.assetid: 3bb6887f-4fc9-452e-bceb-35fe26844ac5
keywords:
- KSCATEGORY_DRM_DESCRAMBLE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_DRM_DESCRAMBLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0890c3ccc5103fedf33892c17bee6a3d593e302d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097247"
---
# <a name="kscategory_drm_descramble"></a>KSCATEGORY_DRM_DESCRAMBLE


KSCATEGORY_DRM_DESCRAMBLE [设备接口类](./overview-of-device-interface-classes.md) 定义为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别，该类别 unscrambles 受 DRM 保护的波形流。

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
<td align="left"><p>KSCATEGORY_DRM_DESCRAMBLE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{FFBB6E3F-CCFE-4D84-90D9-421418B03A8E}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_DRM_DESCRAMBLE 的实例，以向操作系统指示设备支持 KSCATEGORY_DRM_DESCRAMBLE 功能类别。

有关此功能类别的详细信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)。

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
<td align="left"><p>在 windows Vista、Windows Server 2003、Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

