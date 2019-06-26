---
title: 换带机 Miniclass 驱动的 DriverEntry 例程
description: 在 Microsoft Windows 2000 中，换带机 miniclass 驱动程序不具有 DriverEntry 例程中，但在 Windows XP 和更高版本操作系统 miniclass 驱动程序必须具有以下特征的 DriverEntry 例程。
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
ms.openlocfilehash: dcd9adc72a8a19d5d29d4a4a8efed931a302b062
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368274"
---
# <a name="driverentry-of-changer-miniclass-drivers-routine"></a>换带机 Miniclass 驱动的 DriverEntry 例程


在 Microsoft Windows 2000 中，换带机 miniclass 驱动程序不具有**DriverEntry**例程，但在 Windows XP 及更高版本 miniclass 驱动程序必须具有的操作系统**DriverEntry**例程替换以下特征。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PVOID Argument1,
  _In_ PVOID Argument2
);
```

<a name="parameters"></a>Parameters
----------

*Argument1* \[中\]  
指向特定于操作系统的信息。

*Argument2* \[中\]  
指向特定于操作系统的信息。

<a name="return-value"></a>返回值
------------

Miniclass 驱动**DriverEntry**例程必须返回返回的值[ **ChangerClassInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerclassinitialize)例程。

<a name="remarks"></a>备注
-------

参数**Argument1**并**Argument2**指向特定于操作系统的信息。 Miniclass 驱动程序应*不*尝试解释这些参数。 相反，它应传递到这些参数**ChangerClassInitialize**例程。

**ChangerClassInitialize**执行大部分 miniclass 驱动程序所需的初始化。 微型驱动程序中的主要任务及其**DriverEntry**例程是加载到其命令处理例程的入口点[ **MCD\_INIT\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/ns-mcd-_mcd_init_data)结构，将传递到此结构的地址**ChangerClassInitialize**例程。

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
<td align="left"><p>Header</p></td>
<td align="left">Mcd.h （包括 Mcd.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerclassinitialize)

[**MCD\_INIT\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/ns-mcd-_mcd_init_data)

 

 






