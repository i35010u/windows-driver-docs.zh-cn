---
title: IDE 控制器微型驱动程序函数的 DriverEntry
description: DriverEntry 初始化微型驱动程序。
keywords:
- DriverEntry 函数存储设备
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
ms.openlocfilehash: 7edc6620e93a4632ab9dab852f84be2ab6806921
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811727"
---
# <a name="driverentry-of-ide-controller-minidriver-function"></a>IDE 控制器微型驱动程序函数的 DriverEntry


**DriverEntry** 初始化微型驱动程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>参数
----------

*DriverObject* \[中\]  
包含指向 IDE 控制器微型驱动程序的驱动程序对象的指针。

*RegistryPath* \[中\]  
指定一个字符串，该字符串指示注册表中驱动程序的配置信息的注册表路径。

<a name="return-value"></a>返回值
------------

**DriverEntry** \_ 如果成功，DRIVERENTRY 将返回状态 SUCCESS; 否则，将返回 [**PciIdeXInitialize**](/previous-versions/windows/hardware/drivers/ff563788(v=vs.85))库例程收到的错误代码。

<a name="remarks"></a>备注
-------

每个控制器微型驱动程序必须具有名为 **DriverEntry** 的例程才能加载。

IDE 控制器微型驱动程序的 **DriverEntry** 例程必须调用 [**PciIdeXInitialize**](/previous-versions/windows/hardware/drivers/ff563788(v=vs.85)) 库例程。 **PciIdeXInitialize** 初始化控制器微型驱动程序的调度表，为 *DriverObject* 分配扩展，并在驱动程序对象的扩展中存储各种值。 必须存储在驱动程序对象扩展中的值包括驱动程序扩展的大小和一个指针，该指针指向用于检索有关 IDE 控制器的信息的控制器微型驱动程序 [**HwIdeXGetControllerProperties**](/previous-versions/windows/hardware/drivers/ff557254(v=vs.85)) 例程。

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
<td align="left"><p>标头</p></td>
<td align="left">Ide .h (包含 Ide .h) </td>
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


[**HwIdeXGetControllerProperties**](/previous-versions/windows/hardware/drivers/ff557254(v=vs.85))

[**IDE \_ 控制器 \_ 属性**](/previous-versions/windows/hardware/drivers/ff559076(v=vs.85))

[**PciIdeXInitialize**](/previous-versions/windows/hardware/drivers/ff563788(v=vs.85))

 

