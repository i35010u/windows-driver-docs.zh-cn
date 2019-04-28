---
title: KSPROPERTY\_AUDIOMODULE 枚举
description: KSPROPERTY\_AUDIOMODULE 枚举定义常数以音频驱动程序用于通信有关合作伙伴的信息定义音频模块。
ms.assetid: 94873A4A-A40F-40A7-B7A2-B693A5253714
keywords:
- KSPROPERTY_AUDIOMODULE 枚举音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9517363545999f73fd52d857139a61a0dbd4513b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332821"
---
# <a name="kspropertyaudiomodule-enumeration"></a>KSPROPERTY\_AUDIOMODULE 枚举


KSPROPERTY\_AUDIOMODULE 枚举定义常数以音频驱动程序用于通信有关合作伙伴的信息定义音频模块。

有关音频模块的详细信息，请参阅[实现音频模块发现](https://msdn.microsoft.com/windows/hardware/drivers/audio/implementing-audio-module-communication)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_AUDIOMODULE_DESCRIPTORS             = 1,
  KSPROPERTY_AUDIOMODULE_COMMAND                 = 2,
  KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID  = 3
} KSPROPERTY_AUDIOMODULE;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_AUDIOMODULE_DESCRIPTORS__"></span><span id="ksproperty_audiomodule_descriptors__"></span>**KSPROPERTY\_AUDIOMODULE\_描述符**   
指定的 ID [ **KSPROPERTY\_AUDIOMODULE\_描述符**](ksproperty-audiomodule-descriptors.md)属性。

<span id="KSPROPERTY_AUDIOMODULE_COMMAND"></span><span id="ksproperty_audiomodule_command"></span>**KSPROPERTY\_AUDIOMODULE\_命令**  
指定的 ID [ **KSPROPERTY\_AUDIOMODULE\_命令**](ksproperty-audiomodule-command.md)属性。

<span id="KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID"></span><span id="ksproperty_audiomodule_notification_device_id"></span>**KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID**  
指定的 ID [ **KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID** ](ksproperty-audiomodule-notification-device-id.md)属性。

<a name="remarks"></a>备注
-------

KS 属性的所有调用必须为非都阻塞因为硬件效果处理链的一部分而不应等待。

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
<td align="left"><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






