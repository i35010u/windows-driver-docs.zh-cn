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
ms.openlocfilehash: 034bd2fb6c439d722a34c0fa8fad4df60471074d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845167"
---
# <a name="driverentry-of-tape-miniclass-driver-routine"></a>磁带 Miniclass 驱动程序例程的 DriverEntry


**DriverEntry**初始化磁带 miniclass 驱动程序。 此例程是必需的。

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

\] 中的*Argument1* \[  
指向磁带 miniclass 驱动程序传递到[**TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclassinitialize)的驱动程序上下文的指针。 上下文信息的格式是特定于 OS 的，不能由便携式磁带 miniclass 驱动程序解释。

\] 中的*Argument2* \[  
指向磁带 miniclass 驱动程序传递到**TapeClassInitialize**的第二个上下文结构的指针。 上下文信息的格式是特定于 OS 的，不能由便携式磁带 miniclass 驱动程序解释。

<a name="return-value"></a>返回值
------------

**DriverEntry**返回通过其对**TapeClassInitialize**的调用返回的值。

<a name="remarks"></a>备注
-------

**DriverEntry**是磁带 miniclass 驱动程序的初始入口点。

由于**TapeClassInitialize**执行大部分必需的驱动程序初始化，因此磁带 miniclass 驱动程序的**DriverEntry**例程的主要任务是分配和填充磁带\_初始\_数据\_EX 结构驱动程序特定的常量和入口点。

**DriverEntry** first 必须调用[**TAPECLASSZEROMEMORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclasszeromemory)以清除磁带\_INIT\_数据\_EX 结构。 然后， **DriverEntry**设置结构中的值和指针。

**DriverEntry**调用**TapeClassInitialize** ，并\_EX 和传递到**DriverEntry**的两个指针（*ARGUMENT1*和*Argument2*）传递磁带\_INIT\_数据的地址。 **TapeClassInitialize**完成驱动程序初始化，并将状态返回给磁带 miniclass 驱动程序的**DriverEntry**例程。 **DriverEntry**返回从**TapeClassInitialize**接收的状态。

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
<td align="left"><p>标头</p></td>
<td align="left">Minitape</td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**磁带\_INIT\_数据\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/ns-minitape-_tape_init_data_ex)

[**TapeClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclassinitialize)

[**TapeClassZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/nf-minitape-tapeclasszeromemory)

[**磁带\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/ne-minitape-_tape_status)

 

 






