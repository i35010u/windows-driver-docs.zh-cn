---
title: WdfDeviceStopIdleWithTag 宏
description: WdfDeviceStopIdleWithTag 宏递增指定的框架设备对象的 power 引用计数，并将驱动程序的当前文件名和行号分配给该引用。 宏还将分配到引用的标记值。
ms.assetid: 792A5EA8-5273-4284-B0EE-01BE1DCB9863
keywords:
- WdfDeviceStopIdleWithTag 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437bce066d1e72167a4b340d37a5cc94e355abc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562289"
---
# <a name="wdfdevicestopidlewithtag-macro"></a>WdfDeviceStopIdleWithTag 宏


\[适用于 KMDF 和 UMDF\]

**WdfDeviceStopIdleWithTag**宏递增指定的框架设备对象的 power 引用计数并将驱动程序的当前文件名和行号分配给该引用。 宏还将分配到引用的标记值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS WdfDeviceStopIdleWithTag(
  [in] WDFDEVICE Device,
  [in] BOOLEAN   WaitForD0,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>Parameters
----------

*设备*\[中\]  
Framework 设备对象的句柄。

*WaitForD0* \[in\]  
一个布尔值，指示何时**WdfDeviceStopIdleWithTag**将返回。 如果 **，则返回 TRUE**，它将返回仅后指定的设备已进入 D0 设备电源状态。 如果**FALSE**，方法将立即返回。

*Tag* \[in\]  
驱动程序定义的一个值，该框架将存储为 power 引用标识标记。

<a name="return-value"></a>返回值
------------

如果操作成功， **WdfDeviceStopIdleWithTag**返回 STATUS_SUCCESS。 如果该驱动程序调用**WdfDeviceStopIdleWithTag**其工作 (D0) 状态的设备时，该方法返回 STATUS_SUCCESS，但不会增加 power 引用计数。

附加返回值包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>STATUS_PENDING</strong></td>
<td><p>以异步方式正在启动设备。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INVALID_DEVICE_STATE</strong></td>
<td><p>该驱动程序不是设备的电源策略所有者。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_POWER_STATE_INVALID</strong></td>
<td><p>设备故障发生，则设备无法进入其 D0 电源状态。</p></td>
</tr>
</tbody>
</table>

 

该方法可能返回其他[NTSTATUS 值](https://msdn.microsoft.com/library/windows/hardware/ff557697)。

如果驱动程序提供了无效的对象句柄，则会发生的 bug 检查。

<a name="remarks"></a>备注
-------

如果您的驱动程序调用**WdfDeviceStopIdleWithTag**递增引用计数，该驱动程序必须调用[ **WdfDeviceResumeIdleWithTag** ](wdfdeviceresumeidlewithtag.md)要递减计数。

调用**WdfDeviceStopIdleWithTag**而不是[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)提供您可以查看中的其他信息 （标记值、 行号和文件名）Microsoft 调试器。 **WdfDeviceStopIdleWithTag**使用驱动程序的当前行号和文件名称。

可以通过查看标记、 行号和文件名称值[ **！ wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)调试器扩展。 调试器扩展显示为一个指针，以及一系列字符的标记值。

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

[**WdfDeviceResumeIdleWithTag**](wdfdeviceresumeidlewithtag.md)

[**WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)

 

 






