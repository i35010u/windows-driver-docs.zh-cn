---
title: 磁带 Miniclass 驱动程序例程的 DriverEntry
description: DriverEntry 初始化磁带 miniclass 驱动程序。 此例程是必需的。
ms.assetid: dc082f31-5ec5-491e-a347-8f8e485c042b
keywords:
- DriverEntry 例程存储设备
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: affa53f1a4dfc90de1e0bf63586a58df1d2b739f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185897"
---
# <a name="driverentry-of-tape-miniclass-driver-routine"></a>磁带 Miniclass 驱动程序例程的 DriverEntry


**DriverEntry** 初始化磁带 miniclass 驱动程序。 此例程是必需的。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
ULONG DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>参数
----------

*Argument1* \[中\]  
指向磁带 miniclass 驱动程序传递到 [**TapeClassInitialize**](/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclassinitialize)的驱动程序上下文的指针。 上下文信息的格式是特定于 OS 的，不能由便携式磁带 miniclass 驱动程序解释。

*Argument2* \[中\]  
指向磁带 miniclass 驱动程序传递到 **TapeClassInitialize**的第二个上下文结构的指针。 上下文信息的格式是特定于 OS 的，不能由便携式磁带 miniclass 驱动程序解释。

<a name="return-value"></a>返回值
------------

**DriverEntry** 返回通过其对 **TapeClassInitialize**的调用返回的值。

<a name="remarks"></a>备注
-------

**DriverEntry** 是磁带 miniclass 驱动程序的初始入口点。

由于 **TapeClassInitialize** 执行大部分必需的驱动程序初始化，因此磁带 miniclass 驱动程序的 **DriverEntry** 例程的主要任务是 \_ \_ \_ 使用特定于驱动程序的常量和入口点分配并填充磁带初始化数据 EX 结构。

**DriverEntry** first 必须调用 [**TAPECLASSZEROMEMORY**](/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclasszeromemory) 以清除磁带 \_ 初始化 \_ 数据 \_ EX 结构。 然后， **DriverEntry**设置结构中的值和指针。

**DriverEntry** 调用 **TAPECLASSINITIALIZE** 并传递磁带 INIT 数据的地址（ \_ 例如） \_ \_ 和传递到 **DriverEntry** (*Argument1* 和 *Argument2*) 的两个指针。 **TapeClassInitialize** 完成驱动程序初始化，并将状态返回给磁带 miniclass 驱动程序的 **DriverEntry** 例程。 **DriverEntry** 返回从 **TapeClassInitialize**接收的状态。

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
<td align="left">“桌面”</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Minitape</td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**磁带 \_ 初始化 \_ 数据（ \_ EX）**](/windows-hardware/drivers/ddi/minitape/ns-minitape-_tape_init_data_ex)

[**TapeClassInitialize**](/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclassinitialize)

[**TapeClassZeroMemory**](/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclasszeromemory)

[**磁带 \_ 状态**](/windows-hardware/drivers/ddi/minitape/ne-minitape-_tape_status)

 

