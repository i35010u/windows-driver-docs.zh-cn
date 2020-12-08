---
title: KSPROPERTY \_ AUDIOENGINE 枚举
description: KSPROPSETID \_ AudioEngine 属性集中包含的属性是由此枚举定义的，并且必须受 KSNODETYPE \_ 音频 \_ 引擎节点支持。
keywords:
- KSPROPERTY_AUDIOENGINE 枚举音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccdefb1b1a21fa2c79bddbd4bf7b71e5d2f3d531
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798945"
---
# <a name="ksproperty_audioengine-enumeration"></a>KSPROPERTY \_ AUDIOENGINE 枚举


[KSPROPSETID \_ AudioEngine](kspropsetid-audioengine.md)属性集中包含的属性是由此枚举定义的，并且必须受 [**KSNODETYPE \_ 音频 \_ 引擎**](ksnodetype-audio-engine.md)节点支持。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_AUDIOENGINE_LFXENABLE               = 0,
  KSPROPERTY_AUDIOENGINE_GFXENABLE               = 1,
  KSPROPERTY_AUDIOENGINE_MIXFORMAT               = 2,
  KSPROPERTY_AUDIOENGINE_DEVICEFORMAT            = 4,
  KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS  = 5,
  KSPROPERTY_AUDIOENGINE_DESCRIPTOR              = 6,
  KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE       = 7,
  KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION     = 8,
  KSPROPERTY_AUDIOENGINE_VOLUMELEVEL             = 9
} KSPROPERTY_AUDIOENGINE;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_AUDIOENGINE_LFXENABLE"></span><span id="ksproperty_audioengine_lfxenable"></span>**KSPROPERTY \_ AUDIOENGINE \_ LFXENABLE**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ LFXENABLE**](ksproperty-audioengine-lfx-enable.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_GFXENABLE"></span><span id="ksproperty_audioengine_gfxenable"></span>**KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE**](ksproperty-audioengine-gfx-enable.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_MIXFORMAT"></span><span id="ksproperty_audioengine_mixformat"></span>**KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT**](ksproperty-audioengine-mixformat.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_DEVICEFORMAT"></span><span id="ksproperty_audioengine_deviceformat"></span>**KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT**](ksproperty-audioengine-deviceformat.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS"></span><span id="ksproperty_audioengine_supporteddeviceformats"></span>**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_DESCRIPTOR"></span><span id="ksproperty_audioengine_descriptor"></span>**KSPROPERTY \_ AUDIOENGINE \_ 描述符**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ 描述符**](ksproperty-audioengine-descriptor.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE"></span><span id="ksproperty_audioengine_buffer_size_range"></span>**KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**](ksproperty-audioengine-buffer-size-limits.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION"></span><span id="ksproperty_audioengine_loopback_protection"></span>**KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ 保护**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ PROTECTION**](ksproperty-audioengine-loopback-protection.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOENGINE_VOLUMELEVEL"></span><span id="ksproperty_audioengine_volumelevel"></span>**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL**  
指定 [**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md) 属性的 ID。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE \_ 音频 \_ 引擎**](ksnodetype-audio-engine.md)

[KSPROPSETID \_ AudioEngine](kspropsetid-audioengine.md)

 

 






