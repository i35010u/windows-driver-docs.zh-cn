---
title: DriverEntry of Miniclass 驱动程序例程
description: 在 Microsoft Windows 2000 中，更换器 miniclass 驱动程序没有 DriverEntry 例程，但在 Windows XP 和更高版本的操作系统中，miniclass 驱动程序必须具有具有以下特征的 DriverEntry 例程。
ms.assetid: f7954e15-f995-44da-92fd-979248c69553
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
ms.openlocfilehash: 6e4221a4eb4881bd4173771c8ae4ea8e2d843727
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191155"
---
# <a name="driverentry-of-changer-miniclass-drivers-routine"></a>DriverEntry of Miniclass 驱动程序例程


在 Microsoft Windows 2000 中，更换器 miniclass 驱动程序没有 **DriverEntry** 例程，但在 Windows XP 和更高版本的操作系统中，miniclass 驱动程序必须具有具有以下特征的 **DriverEntry** 例程。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>参数
----------

*Argument1* \[中\]  
指向特定于操作系统的信息的指针。

*Argument2* \[中\]  
指向特定于操作系统的信息的指针。

<a name="return-value"></a>返回值
------------

Miniclass 驱动程序的 **DriverEntry** 例程必须返回 [**ChangerClassInitialize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize) 例程返回的值。

<a name="remarks"></a>注解
-------

参数 **Argument1** 和 **Argument2** 指向特定于操作系统的信息。 Miniclass 驱动程序 *不* 应尝试解释这些参数。 相反，它应将这些参数传递到 **ChangerClassInitialize** 例程。

**ChangerClassInitialize** 执行 miniclass 驱动程序所需的大部分初始化。 微型驱动程序在其 **DriverEntry** 例程中的主要任务是将入口点加载到其命令处理例程，并将其传递到 [**MCD \_ INIT \_ 数据**](/windows-hardware/drivers/ddi/mcd/ns-mcd-_mcd_init_data) 结构，并将此结构的地址传递到 **ChangerClassInitialize** 例程。

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
<td align="left"><p>Header</p></td>
<td align="left">Mcd (包含 Mcd) </td>
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


[**ChangerClassInitialize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize)

[**MCD \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/mcd/ns-mcd-_mcd_init_data)

 

