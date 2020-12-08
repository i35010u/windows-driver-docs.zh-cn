---
title: KSPROPERTY \_ AUDIOMODULE 枚举
description: KSPROPERTY \_ AUDIOMODULE 枚举定义音频驱动程序用于传达有关合作伙伴定义的音频模块的信息的常量。
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
ms.openlocfilehash: fd4fe27f7a5c3c5984edd41aa6307835ae6688da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798919"
---
# <a name="ksproperty_audiomodule-enumeration"></a>KSPROPERTY \_ AUDIOMODULE 枚举


KSPROPERTY \_ AUDIOMODULE 枚举定义音频驱动程序用于传达有关合作伙伴定义的音频模块的信息的常量。

有关音频模块的详细信息，请参阅 [实现音频模块发现](./implementing-audio-module-communication.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_AUDIOMODULE_DESCRIPTORS             = 1,
  KSPROPERTY_AUDIOMODULE_COMMAND                 = 2,
  KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID  = 3
} KSPROPERTY_AUDIOMODULE;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_AUDIOMODULE_DESCRIPTORS__"></span><span id="ksproperty_audiomodule_descriptors__"></span>**KSPROPERTY \_ AUDIOMODULE \_ 描述符**   
指定 [**KSPROPERTY \_ AUDIOMODULE \_ 描述符**](ksproperty-audiomodule-descriptors.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOMODULE_COMMAND"></span><span id="ksproperty_audiomodule_command"></span>**KSPROPERTY \_ AUDIOMODULE \_ 命令**  
指定 [**KSPROPERTY \_ AUDIOMODULE \_ 命令**](ksproperty-audiomodule-command.md) 属性的 ID。

<span id="KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID"></span><span id="ksproperty_audiomodule_notification_device_id"></span>**KSPROPERTY \_ AUDIOMODULE \_ 通知 \_ 设备 \_ ID**  
指定 [**KSPROPERTY \_ AUDIOMODULE \_ NOTIFICATION \_ 设备 \_ id**](ksproperty-audiomodule-notification-device-id.md) 属性的 id。

<a name="remarks"></a>备注
-------

所有 KS 属性调用都必须是非阻塞的，因为硬件效果是处理链的一部分并且不应等待。

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
<td align="left"><p>Windows 10 版本 1703</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID \_ AudioModule](kspropsetid-audiomodule.md)

 

