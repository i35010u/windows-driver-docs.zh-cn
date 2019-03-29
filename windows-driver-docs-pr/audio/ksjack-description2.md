---
title: KSJACK\_DESCRIPTION2 结构
description: KSJACK\_DESCRIPTION2 结构指定的功能和支持插孔在场检测 jack 的当前状态。
ms.assetid: 0db29870-20d0-459b-a531-3dea5d073183
keywords:
- KSJACK_DESCRIPTION2 结构音频设备
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
ms.openlocfilehash: 283100a9053b80de46afa42697bf8fe84f947d9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566592"
---
# <a name="ksjackdescription2-structure"></a>KSJACK\_DESCRIPTION2 结构


`KSJACK_DESCRIPTION2`结构指定的功能和支持插孔在场检测 jack 的当前状态。

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
指定的 DWORD 参数的低 16 位。 此参数指示 jack 是当前处于活动状态、 流式处理、 处于空闲状态，或未准备好的硬件。

**JackCapabilities**  
指定的 DWORD 参数的低 16 位。 此参数是一个标志，它指示 jack 的功能。 此标志可设置为下表中的值之一。

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
<td align="left"><p>JACKDESC2_PRESENCE_DETECT_CAPABILITY (0x00000001)</p></td>
<td align="left"><p>Jack 支持 jack 在场检测。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>JACKDESC2_DYNAMIC_FORMAT_CHANGE_CAPABILITY (0x00000002)</p></td>
<td align="left"><p>Jack 支持动态格式更改。</p></td>
</tr>
</tbody>
</table>

 

有关动态格式更改的详细信息，请参阅[动态格式更改](https://msdn.microsoft.com/library/windows/hardware/ff536371)。

<a name="remarks"></a>备注
-------

如果音频设备缺少 jack 在场检测**IsConnected**的成员[ **KSJACK\_说明**](ksjack-description.md)结构必须始终设置为 **，则返回 TRUE**。 若要删除此双的含义而得出的多义性 **，则返回 TRUE**值**IsConnected**，客户端应用程序可以调用[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)以读取**JackCapabilities**标志的`KSJACK_DESCRIPTION2`结构。 如果此标志有 JACKDESC2\_是否存在\_检测\_功能位集，它指示终结点，实际上支持 jack 在场检测。 在这种情况下，返回值**IsConnected**成员可以解释为准确反映 jack 插入状态。

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
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK\_说明**](ksjack-description.md)

[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)

 

 






