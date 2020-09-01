---
title: KSRTAUDIO \_ BUFFER \_ 属性结构
description: KSRTAUDIO \_ buffer \_ 属性结构将缓冲区基址和请求的缓冲区大小追加到 KSPROPERTY 结构。 此结构由客户端用于请求通过 KSPROPERTY RTAUDIO 缓冲区分配音频缓冲区 \_ \_ 。
ms.assetid: 6fc33d5d-5d7e-4d04-a9b0-864cba961077
keywords:
- KSRTAUDIO_BUFFER_PROPERTY 构造音频设备
- PKSRTAUDIO_BUFFER_PROPERTY 结构指针音频设备
topic_type:
- apiref
api_name:
- KSRTAUDIO_BUFFER_PROPERTY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae13cedb48888d2ad101fe211f09b547336191d1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208829"
---
# <a name="ksrtaudio_buffer_property-structure"></a>KSRTAUDIO \_ BUFFER \_ 属性结构


KSRTAUDIO \_ buffer \_ 属性结构将缓冲区基址和请求的缓冲区大小追加到 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构。 此结构由客户端用于请求通过 [**KSPROPERTY \_ RTAUDIO \_ 缓冲区**](ksproperty-rtaudio-buffer.md)分配音频缓冲区。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct {
  KSPROPERTY Property;
  PVOID      BaseAddress;
  ULONG      RequestedBufferSize;
} KSRTAUDIO_BUFFER_PROPERTY, *PKSRTAUDIO_BUFFER_PROPERTY;
```

<a name="members"></a>成员
-------

**属性**  
在调用 KSPROPERTY RTAUDIO 缓冲区之前，客户端正确初始化的 KSPROPERTY 结构 \_ \_ 。

**BaseAddress**  
指定所需的缓冲区基址。 除非客户端指定基址，否则此参数设置为 **NULL**。

**RequestedBufferSize**  
指定所需的缓冲区大小（以字节为单位）。 驱动程序将返回已分配缓冲区的实际大小，该大小由它返回的 [**KSRTAUDIO \_ 缓冲区**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer) 结构返回。

<a name="remarks"></a>备注
-------

KSPROPERTY \_ RTAUDIO \_ 缓冲区请求使用 KSRTAUDIO \_ 缓冲区 \_ 属性结构来描述客户端请求的循环缓冲区。 驱动程序返回一个 KSRTAUDIO \_ 缓冲区结构，用于描述实际分配的缓冲区。

客户端写入到 **RequestedBufferSize** 成员中的值不在驱动程序上绑定。 但是，驱动程序必须指定尽可能接近于所请求大小的缓冲区大小，从而考虑驱动程序本身的缓冲区大小约束。 如果硬件无法处理请求的大小，或者系统内存不足，则驱动程序将分配不同大小的缓冲区。 例如，驱动程序分配的缓冲区不小于内存页，或者将缓冲区大小向下舍入到下一个整个示例块。 此外，如果系统内存不足，驱动程序将分配一个小于请求大小的缓冲区。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

