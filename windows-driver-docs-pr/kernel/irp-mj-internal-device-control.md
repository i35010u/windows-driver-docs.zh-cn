---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: 通常，任何支持内部设备控制请求的现有驱动程序的替换都应在 DispatchInternalDeviceControl 例程中处理此请求。
ms.date: 08/12/2017
ms.assetid: fb3d4534-9c6f-4956-b702-5752f9798600
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: ccb75ac674b75d581212501f3dbfeb71aeb46a10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828119"
---
# <a name="irp_mj_internal_device_control"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


通常，任何支持内部设备控制请求的现有驱动程序的替换都应在[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理此请求。 此类驱动程序必须支持与它所替换的驱动程序相同的一组内部 i/o 控制代码。 否则，现有的高级驱动程序可能无法与新的驱动程序一起工作。

需要用来替换特定较低级别系统驱动程序的驱动程序来处理此请求。 例如，系统并行端口驱动程序的替代必须继续支持现有的并行类驱动程序。 请注意，不能替换处理此请求的某些系统驱动程序，特别是系统提供的 SCSI 和视频端口驱动程序。

<a name="when-sent"></a>发送时间
---------

Create 请求成功完成之后的任何时间。

## <a name="input-parameters"></a>输入参数


I/o 控制代码包含在 IRP 的 i/o 堆栈位置的**DeviceIoControl. IoControlCode**中。

其他输入参数取决于 i/o 控制代码的值。 有关详细信息，请参阅[I/o 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)。

## <a name="output-parameters"></a>输出参数


输出参数取决于 i/o 控制代码的值。 有关详细信息，请参阅[I/o 控制代码的缓冲区说明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)。

<a name="operation"></a>操作
---------

当另一个驱动程序调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)或[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)来创建请求时，驱动程序会接收**IRP\_MJ\_内部\_设备\_控制**请求。

已为成对的和分层的内核模式驱动程序（如通过端口驱动程序分层的一个或多个类驱动程序）之间的通信定义了此 i/o 控制代码。 较高级别的驱动程序通过设备或驱动程序特定的 i/o 控制代码设置 Irp，并从下一个较低版本的驱动程序请求支持。

请求的操作是特定于设备或驱动程序的。

有关 IRP\_MJ 的 i/o 控制代码的一般信息[ **\_设备\_控制**](irp-mj-device-control.md)或**IRP\_MJ\_内部\_设备\_控制**请求，请参阅[使用 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)。 另请参阅[特定于设备类型的 I/o 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-type-specific-i-o-requests)。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

 

 




