---
title: KSRTAUDIO\_缓冲区\_属性结构
description: KSRTAUDIO\_缓冲区\_属性结构会追加到 KSPROPERTY 结构缓冲区基址和请求的缓冲区大小。 通过 KSPROPERTY 音频缓冲区的请求分配到客户端使用此结构\_RTAUDIO\_缓冲区。
ms.assetid: 6fc33d5d-5d7e-4d04-a9b0-864cba961077
keywords:
- KSRTAUDIO_BUFFER_PROPERTY 结构音频设备
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
ms.openlocfilehash: b26129dcbbdafe2b09690ae682e42975c3954d2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360473"
---
# <a name="ksrtaudiobufferproperty-structure"></a>KSRTAUDIO\_缓冲区\_属性结构


KSRTAUDIO\_缓冲区\_属性结构追加缓冲区基址和到请求的缓冲区大小[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构。 通过音频缓冲区的请求分配到客户端使用此结构[ **KSPROPERTY\_RTAUDIO\_缓冲区**](ksproperty-rtaudio-buffer.md)。

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
客户端适当地初始化之前调用 KSPROPERTY KSPROPERTY 结构\_RTAUDIO\_缓冲区。

**BaseAddress**  
指定所需的缓冲区的基址。 除非客户端指定基址，此参数设置为**NULL**。

**RequestedBufferSize**  
以字节为单位指定所需的缓冲区大小。 驱动程序将返回分配的缓冲区中的实际大小[ **KSRTAUDIO\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer)它将返回的结构。

<a name="remarks"></a>备注
-------

KSPROPERTY\_RTAUDIO\_缓冲请求使用 KSRTAUDIO\_缓冲区\_属性结构来描述循环缓冲区，客户端请求。 该驱动程序返回 KSRTAUDIO\_缓冲区结构来描述实际分配的缓冲区。

客户端将写入到的值**RequestedBufferSize**成员不绑定该驱动程序。 但是，该驱动程序必须指定缓冲区大小是尽可能接近到请求的大小，考虑到对驱动程序本身的缓冲区大小约束。 如果硬件不能处理请求的大小或系统处于内存过低，则该驱动程序分配不同大小的缓冲区。 例如，驱动程序分配一个缓冲区，不小于内存页上，或者它将舍入到下一步的整个示例块的缓冲区大小。 此外，如果系统内存不足，驱动程序会分配的缓冲区，则小于所请求的大小。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





