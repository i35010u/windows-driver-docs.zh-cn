---
title: RxNewMapUserBuffer 函数
description: RxNewMapUserBuffer 返回用于低 i/o 的用户缓冲区地址。
ms.assetid: 90ab7793-55ed-47f7-b55d-f4205488796c
keywords:
- RxNewMapUserBuffer 函数可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- RxNewMapUserBuffer
api_location:
- rxprocs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3e98730bf8888210995c9fc5bedd6b1bb45bd9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840975"
---
# <a name="rxnewmapuserbuffer-function"></a>RxNewMapUserBuffer 函数


**RxNewMapUserBuffer**返回用于低 i/o 的用户缓冲区地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID RxNewMapUserBuffer(
  _In_ PRX_CONTEXT RxContext
);
```

<a name="parameters"></a>参数
----------

\] 中的*RxContext* \[  
指向 RX\_此请求的上下文结构的指针。

<a name="return-value"></a>返回值
------------

**RxNewMapUserBuffer**在成功时返回映射的地址指针，否则返回**NULL** 。

<a name="remarks"></a>备注
-------

如果存在 MDL，则假定 MDL 描述用户缓冲区，并且**RxNewMapUserBuffer**返回 mdl 的系统地址。 否则， **RxNewMapUserBuffer**将直接返回用户缓冲区。

**RxNewMapUserBuffer**例程检查*RxContext*变量的**CurrentIrp**-&gt;**MdlAddress**成员是否为**NULL** ，并返回**CurrentIrp**-&gt;**UserBuffer**出现这种情况时*RxContext*变量的成员。 如果**CurrentIrp**-&gt;**MdlAddress**成员不为**NULL**，则**RxNewMapUserBuffer**将调用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)以从 IRP 返回 MDL。

请注意， **RxNewMapUserBuffer**例程仅适用于 windows XP 和 windows 2000。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>RxNewMapUserBuffer 例程仅在 Windows XP 和 Windows 2000 上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Rxprocs （包括 Rxcontx 或 Rxprocs）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**RxLowIoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)

[**RxLowIoGetBufferAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)

[**RxMapSystemBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)

[**RX\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/ns-rxcontx-_rx_context)

 

 






