---
title: DriverEntry 的 IDE 控制器微型驱动程序函数
description: DriverEntry 初始化微型驱动程序。
ms.assetid: 124f6273-ab15-426b-abce-a4d8e68e09c7
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
ms.openlocfilehash: 4a62edaf8cce48213db00d6110d825b839330a64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384838"
---
# <a name="driverentry-of-ide-controller-minidriver-function"></a>DriverEntry 的 IDE 控制器微型驱动程序函数


**DriverEntry**初始化微型驱动程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>Parameters
----------

*DriverObject* \[in\]  
包含指向 IDE 控制器微型驱动程序的驱动程序对象的指针。

*RegistryPath* \[in\]  
指定一个字符串，指示在注册表中的驱动程序的配置信息的注册表路径。

<a name="return-value"></a>返回值
------------

**DriverEntry**将返回状态\_如果成功; 否则它将返回从收到的错误代码，则 SUCCESS [ **PciIdeXInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff563788)库例程。

<a name="remarks"></a>备注
-------

每个控制器微型驱动程序必须具有名为的例程**DriverEntry**才能加载。

IDE 控制器微型驱动程序的**DriverEntry**例程必须调用[ **PciIdeXInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff563788)库例程。 **PciIdeXInitialize**初始化控制器微型驱动程序的调度表、 分配的扩展*DriverObject*，并将不同的值存储在驱动程序对象的扩展。 必须存储在驱动程序对象的扩展中的值包括驱动程序扩展和控制器微型驱动程序的指针的大小[ **HwIdeXGetControllerProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff557254)检索的例程有关 IDE 控制器的信息。

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
<td align="left">Ide.h （包括 Ide.h）</td>
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


[**HwIdeXGetControllerProperties**](https://msdn.microsoft.com/library/windows/hardware/ff557254)

[**IDE\_控制器\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff559076)

[**PciIdeXInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff563788)

 

 






