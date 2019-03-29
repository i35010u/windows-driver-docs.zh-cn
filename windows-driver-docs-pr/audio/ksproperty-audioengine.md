---
title: KSPROPERTY\_AUDIOENGINE 枚举
description: KSPROPSETID 中包含的属性\_AudioEngine 属性集由此枚举定义，并且必须受 KSNODETYPE\_音频\_引擎节点。
ms.assetid: F20C05A3-C8A0-4061-93B9-03FD19D37C82
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
ms.openlocfilehash: 1a893fe02c06fdb02d1c54f6d7487724def732f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576666"
---
# <a name="kspropertyaudioengine-enumeration"></a>KSPROPERTY\_AUDIOENGINE 枚举


中包含的属性[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)属性集由此枚举定义，并且必须受[ **KSNODETYPE\_音频\_引擎**](ksnodetype-audio-engine.md)节点。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_AUDIOENGINE_LFXENABLE               = 0,
  KSPROPERTY_AUDIOENGINE_GFXENABLE               = 1,
  KSPROPERTY_AUDIOENGINE_MIXFORMAT               = 2,
  KSPROPERTY_AUDIOENGINE_DEVICEFORMAT            = 4,
  KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS  = 5,
  KSPROPERTY_AUDIOENGINE_DESCRIPTOR              = 6,
  KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE       = 7,
  KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION     = 8,
  KSPROPERTY_AUDIOENGINE_VOLUMELEVEL             = 9
} KSPROPERTY_AUDIOENGINE;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_AUDIOENGINE_LFXENABLE"></span><span id="ksproperty_audioengine_lfxenable"></span>**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_LFXENABLE** ](ksproperty-audioengine-lfx-enable.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_GFXENABLE"></span><span id="ksproperty_audioengine_gfxenable"></span>**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_GFXENABLE** ](ksproperty-audioengine-gfx-enable.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_MIXFORMAT"></span><span id="ksproperty_audioengine_mixformat"></span>**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_MIXFORMAT** ](ksproperty-audioengine-mixformat.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_DEVICEFORMAT"></span><span id="ksproperty_audioengine_deviceformat"></span>**KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT** ](ksproperty-audioengine-deviceformat.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS"></span><span id="ksproperty_audioengine_supporteddeviceformats"></span>**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS** ](ksproperty-audioengine-supporteddeviceformats.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_DESCRIPTOR"></span><span id="ksproperty_audioengine_descriptor"></span>**KSPROPERTY\_AUDIOENGINE\_描述符**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_描述符**](ksproperty-audioengine-descriptor.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE"></span><span id="ksproperty_audioengine_buffer_size_range"></span>**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**](ksproperty-audioengine-buffer-size-limits.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION"></span><span id="ksproperty_audioengine_loopback_protection"></span>**KSPROPERTY\_AUDIOENGINE\_LOOPBACK\_PROTECTION**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_环回\_保护**](ksproperty-audioengine-loopback-protection.md)属性。

<span id="KSPROPERTY_AUDIOENGINE_VOLUMELEVEL"></span><span id="ksproperty_audioengine_volumelevel"></span>**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**  
指定的 ID [ **KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL** ](ksproperty-audioengine-volumelevel.md)属性。

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
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_AUDIO\_ENGINE**](ksnodetype-audio-engine.md)

[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)

 

 






