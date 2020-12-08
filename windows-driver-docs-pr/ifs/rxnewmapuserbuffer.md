---
title: RxNewMapUserBuffer 函数
description: RxNewMapUserBuffer 返回用于低 i/o 的用户缓冲区地址。
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
ms.openlocfilehash: d8832283707a10078b34cba3b85959dd5d0bca27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789911"
---
# <a name="rxnewmapuserbuffer-function"></a>RxNewMapUserBuffer 函数


**RxNewMapUserBuffer** 返回用于低 i/o 的用户缓冲区地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID RxNewMapUserBuffer(
  _In_ PRX_CONTEXT RxContext
);
```

<a name="parameters"></a>参数
----------

*RxContext* \[中\]  
指向此请求的 RX \_ 上下文结构的指针。

<a name="return-value"></a>返回值
------------

**RxNewMapUserBuffer** 在成功时返回映射的地址指针，否则返回 **NULL** 。

<a name="remarks"></a>备注
-------

如果存在 MDL，则假定 MDL 描述用户缓冲区，并且 **RxNewMapUserBuffer** 返回 mdl 的系统地址。 否则， **RxNewMapUserBuffer** 将直接返回用户缓冲区。

**RxNewMapUserBuffer** 例程检查 RxContext 变量的 **CurrentIrp** - &gt; **MdlAddress** 成员是否为 *RxContext* **NULL** ，并在出现 **CurrentIrp** - &gt; 这种情况时返回 *CurrentIrp* 变量的 UserBuffer **RxContext** 成员。 如果 **CurrentIrp** - &gt; **MdlAddress** 成员不为 **NULL**，则 **RxNewMapUserBuffer** 将调用 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)以从 IRP 返回 MDL。

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
<td align="left">台式机</td>
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

## <a name="see-also"></a>请参阅


[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)

[**RxLowIoCompletion**](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)

[**RxLowIoGetBufferAddress**](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)

[**RxMapSystemBuffer**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)

[**RX \_ 上下文**](/windows-hardware/drivers/ddi/rxcontx/ns-rxcontx-_rx_context)

 

