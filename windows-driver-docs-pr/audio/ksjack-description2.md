---
title: KSJACK\_DESCRIPTION2 结构
description: KSJACK\_DESCRIPTION2 结构指定支持插孔存在检测的插孔的功能和当前状态。
ms.assetid: 0db29870-20d0-459b-a531-3dea5d073183
keywords:
- KSJACK_DESCRIPTION2 构造音频设备
- PKSJACK_DESCRIPTION2 结构指针音频设备
topic_type:
- apiref
api_name:
- KSJACK_DESCRIPTION2
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dee72cbc15d6cb28cb384aa644143c283b0c7f2
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925550"
---
# <a name="ksjack_description2-structure"></a>KSJACK\_DESCRIPTION2 结构


`KSJACK_DESCRIPTION2`结构指定支持插孔存在检测的插孔的功能和当前状态。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _tagKSJACK_DESCRIPTION2 {
  DWORD DeviceStateInfo;
  DWORD JackCapabilities;
} KSJACK_DESCRIPTION2, *PKSJACK_DESCRIPTION2;
```

<a name="members"></a>成员
-------

**DeviceStateInfo**  
指定 DWORD 参数的低16位。 此参数指示插孔当前处于活动状态、流式处理、空闲状态还是未就绪。

**JackCapabilities**  
指定 DWORD 参数的低16位。 此参数是一个标志，它指示了插孔的功能。 此标志可设置为下表中的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>标志</strong></p></td>
<td align="left"><p><strong>含义</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>JACKDESC2_PRESENCE_DETECT_CAPABILITY （0x00000001）</p></td>
<td align="left"><p>插座支持插孔状态检测。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>JACKDESC2_DYNAMIC_FORMAT_CHANGE_CAPABILITY （0x00000002）</p></td>
<td align="left"><p>插座支持动态格式更改。</p></td>
</tr>
</tbody>
</table>

 

有关动态格式更改的详细信息，请参阅[动态格式更改](https://docs.microsoft.com/windows-hardware/drivers/audio/dynamic-format-change)。

<a name="remarks"></a>备注
-------

如果音频设备缺少插孔状态检测，则必须始终将[**KSJACK\_说明**](ksjack-description.md)结构的**connectionmultiplexer.isconnected**成员设置为**TRUE**。 为了消除**connectionmultiplexer.isconnected**的**TRUE**值这一双重含义产生的多义性，客户端应用程序可以调用[IKsJackDescription2：： GetJackDescription2](https://docs.microsoft.com/windows/win32/api/devicetopology/nf-devicetopology-iksjackdescription2-getjackdescription2)来读取`KSJACK_DESCRIPTION2`结构的**JackCapabilities**标志。 如果此标志具有 JACKDESC2\_的 "\_检测\_功能位" 设置，则表示端点确实支持插孔状态检测。 在这种情况下，可以解释**connectionmultiplexer.isconnected**成员的返回值，以准确反映插孔的插入状态。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK\_说明**](ksjack-description.md)

[IKsJackDescription2::GetJackDescription2](https://docs.microsoft.com/windows/win32/api/devicetopology/nf-devicetopology-iksjackdescription2-getjackdescription2)

 

 






