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
ms.openlocfilehash: 6ebe2849585aff74cc12d9010fd1a57b5a3b60ed
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062992"
---
# <a name="rxnewmapuserbuffer-function"></a>RxNewMapUserBuffer 函数


**RxNewMapUserBuffer** 返回用于低 i/o 的用户缓冲区地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID RxNewMapUserBuffer(
  _In_ PRX_CONTEXT RxContext
);
```

<a name="parameters"></a>parameters
----------

*RxContext* \[中\]  
指向此请求的 RX \_ 上下文结构的指针。

<a name="return-value"></a>返回值
------------

**RxNewMapUserBuffer** 在成功时返回映射的地址指针，否则返回 **NULL** 。

<a name="remarks"></a>备注
-------

如果存在 MDL，则假定 MDL 描述用户缓冲区，并且 **RxNewMapUserBuffer**返回 mdl 的系统地址。 否则， **RxNewMapUserBuffer**将直接返回用户缓冲区。

**RxNewMapUserBuffer**例程检查 RxContext 变量的**CurrentIrp** - &gt; **MdlAddress**成员是否为*RxContext* **NULL** ，并在出现**CurrentIrp** - &gt; 这种情况时返回*CurrentIrp*变量的 UserBuffer**RxContext**成员。 如果**CurrentIrp** - &gt; **MdlAddress**成员不为**NULL**，则**RxNewMapUserBuffer**将调用[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)以从 IRP 返回 MDL。

请注意， **RxNewMapUserBuffer** 例程仅适用于 windows XP 和 windows 2000。

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
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>RxNewMapUserBuffer 例程仅在 Windows XP 和 Windows 2000 上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Rxprocs (包含 Rxcontx 或 Rxprocs) </td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)

[**RxLowIoCompletion**](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)

[**RxLowIoGetBufferAddress**](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)

[**RxMapSystemBuffer**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)

[**RX \_ 上下文**](/windows-hardware/drivers/ddi/rxcontx/ns-rxcontx-_rx_context)

 

