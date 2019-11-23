---
title: 处理设备电源策略所有者中的系统 Query-Power IRP
description: 处理设备电源策略所有者中的系统 Query-Power IRP
ms.assetid: 680e3be2-63d9-4d79-a7c0-422e852e9347
keywords:
- 查询-power Irp WDK 电源管理
- 设备电源策略所有者 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64773b960d56742137fa923da852d4ebce48355d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838680"
---
# <a name="handling-a-system-query-power-irp-in-a-device-power-policy-owner"></a>处理设备电源策略所有者中的系统 Query-Power IRP





当设备电源策略所有者收到[**IRP\_MN\_QUERY\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)系统电源状态的电源时，它会通过传递查询来做出响应，并在[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中发送**IRP\_MN\_查询\_** 设备电源状态。 当堆栈中的所有驱动程序都完成了设备查询后，设备电源策略所有者将完成系统查询。

设备电源策略所有者应在其[DispatchPower 例程](dispatchpower-routines.md)中执行以下步骤来响应系统查询：

1.  调用[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保驱动程序未收到 PnP [**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)在处理 power IRP 时删除\_设备请求。

    如果**IoAcquireRemoveLock**返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 IRP 并返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，并调用**IOCOMPLETEREQUEST**来完成 IRP，并返回失败状态。

2.  请确保驱动程序可以支持查询的系统电源状态，如[筛选器或函数驱动程序中的 "系统查询失败" 中](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)所述。 如果没有，请按照该部分所述，使用失败状态完成 IRP。

    但是，如果为 S4 设备启用了唤醒功能但无法将系统从休眠状态唤醒，则驱动程序不得对 S4 （**PowerSystemHibernate**）的查询失败。 在这种情况下，驱动程序的电源策略所有者（发送[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)）必须取消等待/唤醒 IRP，然后成功进行系统查询。 有关详细信息，请参阅[取消等待/唤醒 IRP](canceling-a-wait-wake-irp.md)。

3.  如果驱动程序可以支持查询的系统电源状态，请调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)。

4.  通过调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)设置下一个较低驱动程序的 IRP 堆栈位置。

5.  在系统查询 power IRP 中设置*IoCompletion*例程。

6.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （在 windows 7 和 windows Vista 中）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （在 Windows SERVER 2003、windows XP 和 windows 2000 中），将 IRP 传递到下一个较低版本的驱动程序。

7.  返回状态\_挂起。

[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程应执行以下操作：

1.  检查**irp-&gt;IoStatus** ，以确保较低版本的驱动程序已成功完成 Irp。 如果较低的驱动程序指定了非成功的 NTSTATUS 值， *IoCompletion*例程应返回 ntstatus 值。

2.  如果较低的驱动程序已成功完成 IRP，请调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)以发送设备查询-power IRP，使其适用于查询的系统电源状态。 如有必要，请参阅[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的设备\_状态阵列，以确定哪些设备电源状态对于查询的系统电源状态有效。

3.  在对**PoRequestPowerIrp**的调用中指定一个回调例程（*CompletionFunction*参数），并在*上下文*区域中传递系统 IRP。

4.  返回状态\_需要更多\_处理\_，以便驱动程序可以在回调例程中完成系统查询 IRP 的处理。

完成 IRP 并运行 IRP 处理过程中设置的所有*IoCompletion*例程后，通过 i/o 管理器，电源管理器将调用电源策略管理器的回调例程（将*CompletionFunction*参数设置为**PoRequestPowerIrp**）。 反过来，回调例程必须执行以下操作：

1.  调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)以启动下一个 power IRP。 （仅限 windows Server 2003、Windows XP 和 Windows 2000。）

2.  完成系统查询-power IRP （调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)），并返回设备查询-power irp 的状态。

3.  调用[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)以释放以前获取的锁。

请记住，设备电源策略所有者不仅发送设备查询，还必须按设备堆栈向下进行处理。 有关详细信息，请参阅[处理 IRP\_MN\_查询\_设备电源状态的电源](handling-irp-mn-query-power-for-device-power-states.md)。

 

 




