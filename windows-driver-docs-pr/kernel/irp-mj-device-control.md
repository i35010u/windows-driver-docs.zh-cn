---
title: IRP_MJ_DEVICE_CONTROL
description: 如果一组系统定义的 I/O 控制代码 (Ioctl) 存在的类型，每个驱动程序特定的设备类型 （请参阅指定设备类型） 的对象属于其设备时需要在 DispatchDeviceControl 例程中，支持此请求。
ms.date: 08/12/2017
ms.assetid: c6436b34-22bd-4e65-bfb0-b2c4d9962e29
keywords:
- IRP_MJ_DEVICE_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: e495c1b63ed6f37115e0381dad9867c5eb6cabbe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368528"
---
# <a name="irpmjdevicecontrol"></a>IRP\_MJ\_DEVICE\_CONTROL


每个驱动程序的设备对象属于特定设备类型 (请参阅[指定设备类型](https://msdn.microsoft.com/library/windows/hardware/ff563821)) 支持在此请求需要[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程中，如果系统定义的 I/O 控制一组代码 (Ioctl) 存在的类型。 Ioctl 的详细信息，请参阅[简介 I/O 控制代码](introduction-to-i-o-control-codes.md)。

更高级别的驱动程序通常将传递到基础设备驱动程序，这些请求。 假定在驱动程序堆栈中的每个设备驱动程序支持此请求，以及一组设备的特定于类型，公共或私有 Ioctl。 有关 Ioctl 特定设备类型的详细信息，请参阅 Microsoft Windows Driver Kit (WDK) 中的设备特定于类型的文档。

<a name="when-sent"></a>发送时间
---------

每当创建请求在成功完成后。

## <a name="input-parameters"></a>输入参数


I/O 控制代码包含在**Parameters.DeviceIoControl.IoControlCode**在驱动程序的 I/O 堆栈 IRP 的位置。

其他输入的参数取决于 I/O 控制代码值。 有关详细信息，请参阅[I/O 控制代码的缓冲区说明](https://msdn.microsoft.com/library/windows/hardware/ff540663)。

## <a name="output-parameters"></a>输出参数


输出参数取决于 I/O 控制代码值。 有关详细信息，请参阅[I/O 控制代码的缓冲区说明](https://msdn.microsoft.com/library/windows/hardware/ff540663)。

<a name="operation"></a>操作
---------

驱动程序收到此 I/O 控制代码，因为用户模式线程已调用 Microsoft Win32 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)函数或更高级别的内核模式驱动程序设置了该请求。 用户模式驱动程序有可能，名为**DeviceIoControl**，并传递在驱动程序定义 (也称为*专用*) I/O 控制代码，以从紧密耦合，请求特定于设备或驱动程序支持内核模式设备驱动程序。

接收的设备 I/O 控制请求时，更高级别的驱动程序通常将传递到下一步低驱动程序 IRP。 但是，有一些例外情况，这种做法。 例如，已将存储从基础端口驱动程序获取的配置信息的类驱动程序可能完成某些 IOCTL\_*XXX*而无需传递到相应端口驱动程序 IRP 的请求.

接收的设备 I/O 控制请求时，设备驱动程序将检查以确定如何满足请求的 I/O 控制代码。 设备驱动程序的最常见的 I/O 控制代码，用于传输少量数据传入或传出的缓冲区**Irp-&gt;AssociatedIrp.SystemBuffer**。

对于 I/O 的常规信息来控制代码**IRP\_MJ\_设备\_控制**或[ **IRP\_MJ\_内部\_设备\_控制**](irp-mj-internal-device-control.md)请求，请参阅[使用的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)。 另请参阅[设备的特定于类型的 I/O 请求](https://msdn.microsoft.com/library/windows/hardware/ff543205)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




