---
title: IRP_MJ_DEVICE_CONTROL
description: 如果设备对象属于特定设备类型，则每个驱动程序都 (参阅指定设备类型) 在 DispatchDeviceControl 例程中支持此请求时，如果该类型存在 (IOCTLs) 的一组系统定义 i/o 控制代码。
ms.date: 08/12/2017
ms.assetid: c6436b34-22bd-4e65-bfb0-b2c4d9962e29
keywords:
- IRP_MJ_DEVICE_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 1289d4ed043d6336f8b94cfbd32a6b1a68686b46
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185619"
---
# <a name="irp_mj_device_control"></a>IRP\_MJ\_DEVICE\_CONTROL


如果设备对象属于特定设备类型，则每个驱动程序都 (参阅 [指定设备类型](./specifying-device-types.md)) 在 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中支持此请求时，如果该类型存在 (IOCTLs) 的一组系统定义 i/o 控制代码。 有关 IOCTLs 的详细信息，请参阅 [I/o 控制代码简介](introduction-to-i-o-control-codes.md)。

较高级别的驱动程序通常将这些请求传递到基础设备驱动程序。 假定驱动程序堆栈中的每个设备驱动程序都支持此请求，以及一组特定于设备类型的、公用或专用 IOCTLs。 有关特定设备类型的 IOCTLs 的详细信息，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的设备类型特定文档。

<a name="when-sent"></a>发送时间
---------

在成功完成创建请求之后的任何时间。

## <a name="input-parameters"></a>输入参数


I/o 控制代码包含在 IRP 的驱动程序 i/o 堆栈位置的 **DeviceIoControl. IoControlCode** 中。

其他输入参数取决于 i/o 控制代码的值。 有关详细信息，请参阅 [I/o 控制代码的缓冲区说明](./buffer-descriptions-for-i-o-control-codes.md)。

## <a name="output-parameters"></a>输出参数


输出参数取决于 i/o 控制代码的值。 有关详细信息，请参阅 [I/o 控制代码的缓冲区说明](./buffer-descriptions-for-i-o-control-codes.md)。

<a name="operation"></a>操作
---------

驱动程序收到此 i/o 控制代码，因为用户模式线程调用了 Microsoft Win32 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数，或更高级别的内核模式驱动程序已设置该请求。 用户模式驱动程序已调用 **DeviceIoControl**，传入驱动程序定义的 (（也称为 *专用*) i/o 控制代码），以从紧密耦合的内核模式设备驱动程序请求特定于设备或驱动程序的支持。

收到设备 i/o 控制请求后，较高级别的驱动程序通常会将 IRP 传递到下一个较低的驱动程序。 但是，这种做法有一些例外情况。 例如，如果类驱动程序的存储配置信息是从基础端口驱动程序获取的，则可能会在 \_ 不将 IRP 向下传递到相应端口驱动程序的情况下完成特定的 IOCTL*XXX*请求。

收到设备 i/o 控制请求后，设备驱动程序将检查 i/o 控制代码以确定如何满足请求。 对于大多数公共 i/o 控制代码，设备驱动程序将少量的数据传入或传出 ** &gt;AssociatedIrp.SystemBuffer**的缓冲区。

有关 **irp \_ mj \_ 设备 \_ 控制** 或 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md) 请求的 I/o 控制代码的常规信息，请参阅 [使用 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)。 另请参阅 [特定于设备类型的 I/o 请求](./device-type-specific-i-o-requests.md)。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

