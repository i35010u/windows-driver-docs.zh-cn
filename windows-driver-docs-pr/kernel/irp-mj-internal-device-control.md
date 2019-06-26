---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: 一般情况下，任何其替代现有驱动程序支持内部设备控制请求应处理此请求 DispatchInternalDeviceControl 例程中。
ms.date: 08/12/2017
ms.assetid: fb3d4534-9c6f-4956-b702-5752f9798600
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 4da0c0d69b381c65da3313b80299eb1152f32e35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370905"
---
# <a name="irpmjinternaldevicecontrol"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


一般情况下，任何其替代现有驱动程序支持内部设备控制请求应处理此请求中的[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 它将替换该驱动程序相同的内部的 I/O 控制代码集必须至少支持这样的驱动程序。 否则，现有的更高级别的驱动程序可能与新的驱动程序不兼容。

将驱动程序所需处理此请求某些较低级别系统为的驱动程序。 例如，替换系统并行端口驱动程序必须继续支持现有的 parallel 类驱动程序。 请注意，某些系统处理此请求的驱动程序不能替换，特别是，系统提供的 SCSI 和视频端口驱动程序。

<a name="when-sent"></a>发送时间
---------

创建请求的成功完成后的任何时间。

## <a name="input-parameters"></a>输入参数


I/O 控制代码包含在**Parameters.DeviceIoControl.IoControlCode**中 I/O 堆栈 IRP 的位置。

其他输入的参数取决于 I/O 控制代码值。 有关详细信息，请参阅[I/O 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)。

## <a name="output-parameters"></a>输出参数


输出参数取决于 I/O 控制代码值。 有关详细信息，请参阅[I/O 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)。

<a name="operation"></a>操作
---------

驱动程序收到**IRP\_MJ\_内部\_设备\_控制**请求时另一个驱动程序拨打[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)或[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)创建请求。

有关配对和分层内核模式驱动程序，例如上层端口驱动程序的一个或多个类驱动程序之间的通信已定义此 I/O 控制代码。 更高级别的驱动程序设置与特定于设备或驱动程序 I/O 控制代码，请求从下一步低驱动程序支持的 Irp。

请求的操作是特定于设备或驱动程序。

对于 I/O 的常规信息来控制代码[ **IRP\_MJ\_设备\_控制**](irp-mj-device-control.md)或**IRP\_MJ\_内部\_设备\_控制**请求，请参阅[使用的 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)。 另请参阅[设备的特定于类型的 I/O 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-type-specific-i-o-requests)。

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


[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

 

 




