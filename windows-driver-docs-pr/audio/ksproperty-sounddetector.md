---
title: KSPROPERTY\_SOUNDDETECTOR 枚举
description: KSPROPERTY\_SOUNDDETECTOR 枚举定义一些常量，用于注册还支持检测程序的音频捕获设备的筛选器。
ms.assetid: 6AF98B06-1531-4AC9-9E32-D812E6EA424C
keywords:
- KSPROPERTY_SOUNDDETECTOR 枚举音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad03404cf7e171704d610bfea6de6c8b124f5154
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332637"
---
# <a name="kspropertysounddetector-enumeration"></a>KSPROPERTY\_SOUNDDETECTOR 枚举


**KSPROPERTY\_SOUNDDETECTOR**枚举定义一些常量，用于注册还支持检测程序的音频捕获设备的筛选器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS  = 1,
  KSPROPERTY_SOUNDDETECTOR_PATTERNS,
  KSPROPERTY_SOUNDDETECTOR_ARMED,
  KSPROPERTY_SOUNDDETECTOR_MATCHRESULT
} KSPROPERTY_SOUNDDETECTOR;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS"></span><span id="ksproperty_sounddetector_supportedpatterns"></span>**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**  
指定的 ID [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS** ](ksproperty-sounddetector-supportedpatterns.md)属性。

<span id="KSPROPERTY_SOUNDDETECTOR_PATTERNS"></span><span id="ksproperty_sounddetector_patterns"></span>**KSPROPERTY\_SOUNDDETECTOR\_PATTERNS**  
指定的 ID [ **KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)属性。

<span id="KSPROPERTY_SOUNDDETECTOR_ARMED"></span><span id="ksproperty_sounddetector_armed"></span>**KSPROPERTY\_SOUNDDETECTOR\_ARMED**  
指定的 ID [ **KSPROPERTY\_SOUNDDETECTOR\_ARMED** ](ksproperty-sounddetector-armed.md)属性。

<span id="KSPROPERTY_SOUNDDETECTOR_MATCHRESULT"></span><span id="ksproperty_sounddetector_matchresult"></span>**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**  
指定的 ID [ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT** ](ksproperty-sounddetector-matchresult.md)属性。

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)

[**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY\_SOUNDDETECTOR\_ARMED**](ksproperty-sounddetector-armed.md)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

 

 






