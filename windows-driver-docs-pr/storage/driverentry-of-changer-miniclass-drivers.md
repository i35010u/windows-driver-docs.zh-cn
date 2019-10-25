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
ms.openlocfilehash: 3b0afece294aa0044e30e1dd2ff6aea78aa3392d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845170"
---
# <a name="driverentry-of-changer-miniclass-drivers-routine"></a>DriverEntry of Miniclass 驱动程序例程


在 Microsoft Windows 2000 中，更换器 miniclass 驱动程序没有**DriverEntry**例程，但在 Windows XP 和更高版本的操作系统中，miniclass 驱动程序必须具有具有以下特征的**DriverEntry**例程。

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

\] 中的*Argument1* \[  
指向特定于操作系统的信息的指针。

\] 中的*Argument2* \[  
指向特定于操作系统的信息的指针。

<a name="return-value"></a>返回值
------------

Miniclass 驱动程序的**DriverEntry**例程必须返回[**ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize)例程返回的值。

<a name="remarks"></a>备注
-------

参数**Argument1**和**Argument2**指向特定于操作系统的信息。 Miniclass 驱动程序*不*应尝试解释这些参数。 相反，它应将这些参数传递到**ChangerClassInitialize**例程。

**ChangerClassInitialize**执行 miniclass 驱动程序所需的大部分初始化。 微型驱动程序在其**DriverEntry**例程中的主要任务是将入口点加载到其命令处理[ **\_例程\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/ns-mcd-_mcd_init_data)结构中，并将此结构的地址传递到**ChangerClassInitialize**例程。

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
<td align="left">Mcd （包括 Mcd）</td>
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


[**ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize)

[**MCD\_INIT\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/ns-mcd-_mcd_init_data)

 

 






