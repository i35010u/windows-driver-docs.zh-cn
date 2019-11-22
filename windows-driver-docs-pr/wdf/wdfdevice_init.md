---
title: WDFDEVICE_INIT 结构
description: WDFDEVICE_INIT 结构是由框架定义和分配的不透明结构。
ms.assetid: 38a8d316-6d66-4c1a-bb1c-93e2893542e8
keywords:
- WDFDEVICE_INIT 结构
ms.date: 02/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5398fd39d785a2ff8602f7081bce12c164def7ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845412"
---
# <a name="wdfdevice_init-structure"></a>WDFDEVICE_INIT 结构


\[适用于 KMDF 和 UMDF\]

**WDFDEVICE_INIT**结构是由框架定义和分配的不透明结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
struct WDFDEVICE_INIT {
  ;      // Reserved.
};
```

<a name="members"></a>成员
----------

函数和筛选器驱动程序接收指向此结构的指针作为[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数的输入，或作为[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)的返回值。

总线驱动程序接收结构指针作为[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数的输入，或接收来自[**WdfPdoInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)的返回值。

驱动程序接收到**WDFDEVICE_INIT**结构后，它会将结构指针传递到初始化函数。
这些函数使用**WDFDEVICE_INIT**结构存储框架用于创建框架设备对象的信息。

若要查找设备初始化方法的文档，请参阅[wdfdevice 标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)。

调用初始化函数后，驱动程序必须调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)来创建框架设备对象。

如果驱动程序已通过调用[**WdfPdoInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)或[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)接收到**WDFDEVICE_INIT**结构，并且驱动程序收到调用初始化函数的错误，则驱动程序必须调用[**WdfDeviceInitFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)而不是[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

你的驱动程序在成功调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之后不得调用[**WdfDeviceInitFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree) 。

**WDFDEVICE_INIT**的结构在版本1.0 和更高版本的 KMDF 中可用。


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
<td>Wdftypes （包括 Wdftypes）</td>
</tr>
</tbody>
</table>


