---
title: WDFDEVICE_INIT 结构
description: WDFDEVICE_INIT 结构是已定义且由框架已分配的不透明结构。
ms.assetid: 38a8d316-6d66-4c1a-bb1c-93e2893542e8
keywords:
- WDFDEVICE_INIT 结构
ms.date: 02/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 26d6a182eb9223512eeaf190ea7ef9f23dfdff5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519693"
---
# <a name="wdfdeviceinit-structure"></a>WDFDEVICE_INIT 结构


\[适用于 KMDF 和 UMDF\]

**WDFDEVICE_INIT**结构是已定义且由框架已分配的不透明结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
struct WDFDEVICE_INIT {
  ;      // Reserved.
};
```

<a name="members"></a>成员
----------

函数和筛选器驱动程序作为输入接收指向此结构的指针[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数或作为返回值从[ **WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)。

总线驱动程序作为输入接收结构指针[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数的返回值，也[ **WdfPdoInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate).

驱动程序收到后**WDFDEVICE_INIT**结构，该结构将指针传递给函数的初始化。
这些函数将使用**WDFDEVICE_INIT**结构来存储该框架用于创建 framework 设备对象的信息。

若要查找设备文档初始化方法，请参阅[wdfdevice.h 标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/)。

在调用函数的初始化后，该驱动程序必须调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建 framework 设备对象。

如果您的驱动程序收到**WDFDEVICE_INIT**调用的结构[ **WdfPdoInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)或者[ **WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)，并且如果该驱动程序收到错误时调用初始化函数，该驱动程序必须调用[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)而不是[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

您的驱动程序不能调用[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)之后在成功调用[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

**WDFDEVICE_INIT**结构是在版本 1.0 和更高版本的 KMDF 中可用。


<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdftypes.h （包括 Wdftypes.h）</td>
</tr>
</tbody>
</table>


