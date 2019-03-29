---
title: WdfDeviceResumeIdleWithTag 宏
description: WdfDeviceResumeIdleWithTag 宏递减 power 引用计数为指定的框架设备对象并将驱动程序的当前文件名和行号分配给该引用。 宏还将分配到引用的标记值。
ms.assetid: 065393BE-CEDF-4B82-AE43-844DDB932DF0
keywords:
- WdfDeviceResumeIdleWithTag 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5eaebdc0dcc63907823799e36db3d63d088f07e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564151"
---
# <a name="wdfdeviceresumeidlewithtag-macro"></a>WdfDeviceResumeIdleWithTag 宏


\[适用于 KMDF 和 UMDF\]

**WdfDeviceResumeIdleWithTag**宏递减 power 引用计数为指定的框架设备对象，并将驱动程序的当前文件名和行号分配给该引用。 宏还将分配到引用的标记值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfDeviceResumeIdleWithTag(
  [in] WDFDEVICE Device,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>Parameters
----------

*设备*\[中\]  
Framework 设备对象的句柄。

*Tag* \[in\]  
驱动程序定义的一个值，该框架将存储为 power 引用标识标记。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供了无效的对象句柄，则会发生的 bug 检查。

<a name="remarks"></a>备注
-------

如果该对象的引用计数变为零，对象可能被删除之前**WdfDeviceResumeIdleWithTag**返回。

调用**WdfDeviceResumeIdleWithTag**而不是[ **WdfDeviceResumeIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546838)提供您可以查看的其他信息 （标记值、 行号和文件名）在 Microsoft 的调试器。 **WdfDeviceResumeIdleWithTag**使用驱动程序的当前行号和文件名称。

可以通过查看标记、 行号和文件名称值[ **！ wdfkd.wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)调试器扩展。

使用[ **！ wdfkd.wdfdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff565703)带有详细标志的和找到的链接[ **！ wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)输出中：

```cpp
kd> !wdfdevice <handle> f 
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.15</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.15</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfdevice.h （包括 Wdf.h）</td>
</tr>
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000.sys (KMDF); WUDFx02000.dll (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[调试在 WDF Power 引用泄漏](https://msdn.microsoft.com/library/windows/hardware/dn965441)

[**WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)

[**WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)

[**WdfDeviceStopIdleWithTag**](wdfdevicestopidlewithtag.md)

 

 






