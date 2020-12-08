---
title: KSPROPERTY \_ 插座枚举
description: KSPROPERTY \_ 插座枚举定义音频插孔结构使用的新属性 id。
keywords:
- KSPROPERTY_JACK 枚举音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24126c7c32e371e85001e87a51d14ddcffa58e33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801207"
---
# <a name="ksproperty_jack-enumeration"></a>KSPROPERTY \_ 插座枚举


`KSPROPERTY_JACK`枚举定义音频插孔结构使用的新属性 id。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_JACK_DESCRIPTION   = 1,
  KSPROPERTY_JACK_DESCRIPTION2  = 2,
  KSPROPERTY_JACK_SINK_INFO     = 3,
  KSPROPERTY_JACK_CONTAINERID
} KSPROPERTY_JACK;
```

<a name="constants"></a>常量
---------

<span id="KSPROPERTY_JACK_DESCRIPTION"></span><span id="ksproperty_jack_description"></span>**KSPROPERTY \_ 插孔 \_ 说明**  
指定 [**KSPROPERTY \_ 插座 \_ DESCRIPTION**](ksproperty-jack-description.md) 属性的 ID。

<span id="KSPROPERTY_JACK_DESCRIPTION2"></span><span id="ksproperty_jack_description2"></span>**KSPROPERTY \_ 插座 \_ DESCRIPTION2**  
指定 [**KSPROPERTY \_ 插座 \_ DESCRIPTION2**](ksproperty-jack-description2.md) 属性的 ID。

<span id="KSPROPERTY_JACK_SINK_INFO"></span><span id="ksproperty_jack_sink_info"></span>**KSPROPERTY \_ 插座 \_ \_ 信息**  
指定 [**KSPROPERTY \_ 插座 \_ \_ 信息**](ksproperty-jack-sink-info.md) 属性的 ID。

<span id="KSPROPERTY_JACK_CONTAINERID"></span><span id="ksproperty_jack_containerid"></span>**KSPROPERTY \_ 插座 \_ CONTAINERID**  
指定 [**KSPROPERTY \_ 插座 \_ CONTAINERID**](ksproperty-jack-containerid.md) 属性的 ID。

<a name="remarks"></a>备注
-------

无

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY \_ 插孔 \_ 说明**](ksproperty-jack-description.md)

 

 






