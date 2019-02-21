---
title: RxNewMapUserBuffer 函数
description: RxNewMapUserBuffer 返回用于低 I/O 的用户缓冲区地址。
ms.assetid: 90ab7793-55ed-47f7-b55d-f4205488796c
keywords:
- RxNewMapUserBuffer 函数可安装文件系统驱动程序
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
ms.openlocfilehash: 3624a1c69f6769ebde201789676e52731a4bac5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541496"
---
# <a name="rxnewmapuserbuffer-function"></a>RxNewMapUserBuffer 函数


**RxNewMapUserBuffer**返回用于低 I/O 的用户缓冲区地址。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PVOID RxNewMapUserBuffer(
  _In_ PRX_CONTEXT RxContext
);
```

<a name="parameters"></a>参数
----------

*RxContext* \[in\]  
指向 RX\_此请求的上下文结构。

<a name="return-value"></a>返回值
------------

**RxNewMapUserBuffer**成功后返回的映射的地址指针或**NULL**失败。

<a name="remarks"></a>备注
-------

如果 MDL 存在，则假设条件是 MDL 描述用户缓冲区，并返回 MDL 的系统地址**RxNewMapUserBuffer**。 否则，将直接通过返回用户缓冲区**RxNewMapUserBuffer**。

**RxNewMapUserBuffer**例程检查**CurrentIrp**-&gt;**MdlAddress**隶属*RxContext*变量是**NULL** ，并返回**CurrentIrp**-&gt;**UserBuffer**隶属*RxContext*变量时出现这种情况。 如果**CurrentIrp**-&gt;**MdlAddress**成员不是**NULL**，然后**RxNewMapUserBuffer**将调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)从 IRP 返回 MDL。

请注意， **RxNewMapUserBuffer**例程才在 Windows XP 和 Windows 2000 上可用。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows XP 和 Windows 2000 上才 RxNewMapUserBuffer 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Rxprocs.h （包括 Rxcontx.h 或 Rxprocs.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)

[**RxLowIoCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff554525)

[**RxLowIoGetBufferAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554529)

[**RxMapSystemBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff554549)

[**RX\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff554751)

 

 






