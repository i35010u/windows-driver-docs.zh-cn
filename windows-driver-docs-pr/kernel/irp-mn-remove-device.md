---
title: IRP_MN_REMOVE_DEVICE
description: 了解 "IRP_MN_REMOVE_DEVICE" 内核模式驱动程序体系结构。 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 0d733cbd-2da8-48a5-afc6-e1e6b8f507a1
keywords:
- IRP_MN_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5a5445a433a7c95d1581eec4585579885d9c5b3a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732973"
---
# <a name="irp_mn_remove_device"></a>IRP \_ MN \_ 删除 \_ 设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x02

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器使用此 IRP 来指示驱动程序删除设备的软件表示形式 (设备对象等) 。 当设备以有序的方式被删除时，PnP 管理器会发送此 IRP (例如，通过 "拔出或弹出硬件程序" 中的用户启动) ，会意外 (用户从其槽拉取设备，而不会出现先前警告) ，或当用户请求更新 () 的驱动程序时。

在 Windows 2000 和更高版本的系统上，如果设备堆栈中的某个驱动程序无法使用 [**irp \_ MN \_ 开始 \_ 设备**](irp-mn-start-device.md) 请求，则 PnP 管理器还会发送此 IRP。

对于有序的设备删除，PnP 管理器会在删除 IRP 之前发送 [**irp \_ MN \_ 查询 \_ 删除 \_ 设备**](irp-mn-query-remove-device.md) 。 在这种情况下，当删除 IRP 到达时，设备处于 "消除挂起" 状态。 对于在 Microsoft Windows 2000 或更高版本上删除的意外设备，PnP 管理器会在删除 IRP 之前发送 [**irp \_ MN \_ 意外 \_ 删除**](irp-mn-surprise-removal.md) 。 在这种情况下，当删除 IRP 到达时，设备处于意外删除状态。 驱动程序还可以在设备启动之前接收删除 IRP。 在这种情况下，当 IRP 到达时，设备处于 "未启动" 状态。

PnP 管理器在 \_ 系统线程的上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/o 状态块


驱动程序必须将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。 驱动程序不能使此 IRP 失败。

<a name="operation"></a>操作
---------

此 IRP 首先由设备堆栈顶部的驱动程序和堆栈中的每个较低的驱动程序处理。

为了响应此 IRP，驱动程序将执行如下任务：关闭设备电源、删除设备的软件表示形式 (设备对象，等等) ，以及释放设备的任何资源。

有关处理此 IRP 的详细信息，请参阅 [处理 irp \_ MN \_ 删除 \_ 设备请求](./handling-an-irp-mn-remove-device-request.md)。 有关支持设备删除的一般信息，请参阅 [删除设备](./removing-a-device-in-a-function-driver.md)。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

如果总线驱动程序检测到 (子 PDOs) 中的一个 (或多个) 子设备已从计算机物理上删除，则总线驱动程序将调用 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations) 来报告 PnP 管理器的更改。 然后，PnP 管理器会为任何已消失的设备发送删除 Irp。

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


[**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)

[**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

[**IRP \_ MN \_ 取消 \_ 删除 \_ 设备**](irp-mn-cancel-remove-device.md)

[**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](irp-mn-query-remove-device.md)

[**IRP \_ MN \_ 意外 \_ 删除**](irp-mn-surprise-removal.md)

