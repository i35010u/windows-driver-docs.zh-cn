---
title: 处理设备电源策略所有者中的系统 Query-Power IRP
description: 处理设备电源策略所有者中的系统 Query-Power IRP
ms.assetid: 680e3be2-63d9-4d79-a7c0-422e852e9347
keywords:
- 查询能耗 Irp WDK 电源管理
- 设备电源策略所有者 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b93e98942f12f3669e69945c9a19d55c24063b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387012"
---
# <a name="handling-a-system-query-power-irp-in-a-device-power-policy-owner"></a>处理设备电源策略所有者中的系统 Query-Power IRP





当设备电源策略所有者收到[ **IRP\_MN\_查询\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)系统电源状态，它响应通过传入下查询，并在[*IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，发送**IRP\_MN\_查询\_POWER**设备电源状态。 设备查询堆栈中的所有驱动程序完成，设备电源策略所有者完成系统查询。

设备电源策略所有者应执行以下步骤其[DispatchPower 例程](dispatchpower-routines.md)响应系统查询：

1.  调用[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)，并传递当前 IRP，以确保该驱动程序不会接收即插即用[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求，而同时处理 IRP 的能力。

    如果**IoAcquireRemoveLock**返回失败状态，该驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)完成 IRP 并返回故障状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，该驱动程序应调用[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)，调用**IoCompleteRequest**完成 IRP，并返回失败状态。

2.  请确保该驱动程序可以支持查询的系统电源状态，如中所述[失败的系统查询能耗 IRP 中一个筛选器或功能驱动程序](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)。 如果没有，那一节中所述完成 IRP 失败状态。

    但是，驱动程序不得失败查询的 S4 (**PowerSystemHibernate**) 如果其设备启用了唤醒，但它无法唤醒从休眠状态系统。 在此情况下，该驱动程序的电源策略所有者 (它发送[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) 必须取消等待/唤醒 IRP 和成功的系统查询。 有关详细信息，请参阅[取消等待/唤醒 IRP](canceling-a-wait-wake-irp.md)。

3.  如果该驱动程序可以支持查询的系统电源状态，调用[ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)。

4.  通过调用设置下一步低驱动程序的 IRP 堆栈位置[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)。

5.  设置*IoCompletion*例行系统查询电源 IRP 中。

6.  调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) （在 Windows 7 和 Windows Vista） 或[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) （在 Windows Server 2003、 Windows XP 和 Windows 2000）若要将 IRP 传递给下一个较低驱动程序。

7.  返回状态\_PENDING。

[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程应执行以下操作：

1.  检查**Irp-&gt;IoStatus.Status**以确保较低的驱动程序已成功完成 IRP。 如果非成功 NTSTATUS 值，指定较低的驱动程序，则*IoCompletion*例程应返回 NTSTATUS 值。

2.  如果较低的驱动程序已成功完成 IRP，调用[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)发送设备是适用于查询的系统的设备电源状态的查询能耗 IRP 电源状态。 如有必要，请查阅设备\_中的状态数组[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构，以确定哪些设备的电源状态适用于在查询的系统电源状态。

3.  指定的回调例程 (*CompletionFunction*参数) 在调用**PoRequestPowerIrp** ，并将传递系统 IRP 中*上下文*区域。

4.  返回状态\_更多\_处理\_必需，以便该驱动程序可以完成的回调例程中的系统查询 IRP 的处理。

IRP 已经完成后和全部*IoCompletion* IRP 处理过程中设置的例程已运行，电源管理器，通过 I/O 管理器、 调用电源策略管理器的回调例程 ( *CompletionFunction*参数**PoRequestPowerIrp**)。 回调例程，反过来，必须执行以下操作：

1.  调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)启动下一个幂 IRP。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅。）

2.  完成系统查询能耗 IRP (调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)) 返回设备的状态与查询能耗 IRP。

3.  调用[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)来释放以前获取的锁。

请记住设备电源策略所有者不仅会将设备查询发送但还必须向下设备堆栈上处理它。 有关详细信息，请参阅[处理 IRP\_MN\_查询\_的电源可用于设备的电源状态](handling-irp-mn-query-power-for-device-power-states.md)。

 

 




