---
title: KSPROPERTY \_ SOUNDDETECTOR 枚举
description: KSPROPERTY \_ SOUNDDETECTOR 枚举定义用于为还支持检测程序的音频捕获设备注册筛选器的常量。
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
ms.openlocfilehash: 475f39f09b4497c750214f361ba20cde5b4a5b48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801165"
---
# <a name="ksproperty_sounddetector-enumeration"></a>KSPROPERTY \_ SOUNDDETECTOR 枚举


**KSPROPERTY \_ SOUNDDETECTOR** 枚举定义用于为还支持检测程序的音频捕获设备注册筛选器的常量。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS  = 1,
  KSPROPERTY_SOUNDDETECTOR_PATTERNS,
  KSPROPERTY_SOUNDDETECTOR_ARMED,
  KSPROPERTY_SOUNDDETECTOR_MATCHRESULT
} KSPROPERTY_SOUNDDETECTOR;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS"></span><span id="ksproperty_sounddetector_supportedpatterns"></span>**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**  
指定 [**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md) 属性的 ID。

<span id="KSPROPERTY_SOUNDDETECTOR_PATTERNS"></span><span id="ksproperty_sounddetector_patterns"></span>**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**  
指定 [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md) 属性的 ID。

<span id="KSPROPERTY_SOUNDDETECTOR_ARMED"></span><span id="ksproperty_sounddetector_armed"></span>**KSPROPERTY \_ SOUNDDETECTOR \_**  
指定 [**KSPROPERTY \_ SOUNDDETECTOR \_**](ksproperty-sounddetector-armed.md) 提供的属性的 ID。

<span id="KSPROPERTY_SOUNDDETECTOR_MATCHRESULT"></span><span id="ksproperty_sounddetector_matchresult"></span>**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**  
指定 [**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**](ksproperty-sounddetector-matchresult.md) 属性的 ID。

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
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID \_ SoundDetector](kspropsetid-sounddetector.md)

[**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

[**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY \_ SOUNDDETECTOR \_**](ksproperty-sounddetector-armed.md)

[**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

 

 






