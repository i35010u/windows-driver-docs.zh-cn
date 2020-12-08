---
title: 系统的电源 IRP
description: 系统的电源 IRP
keywords:
- power Irp WDK 内核，系统
- 系统电源 Irp WDK 内核
- IRP_MJ_POWER
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- 浪涌电源 WDK 内核
- 系统浪涌电源 WDK 内核
- 更改电源状态 WDK 内核
- reaffirming 电源状态
- 空闲超时 WDK 电源管理
- 电池过期后电源管理
- 电池电量寿命-电源管理
- 用户请求电源更改 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec48426d03d9e573b67bb9cbaf62189fee8b1ae5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803799"
---
# <a name="power-irps-for-the-system"></a>系统的电源 IRP





*系统电源 IRP* 指定主要 Irp 代码 [**irp \_ MJ \_ 功能**](./irp-mj-power.md)，下面列出的一个小电源 IRP 代码，以及 IRP 堆栈的 **SystemPowerState** 成员中的值 **。** 只有电源管理器可以发送此类 IRP;驱动程序无法发送系统电源 IRP。

由于以下原因之一，电源管理器会发送系统电源 IRP：

-   更改系统电源状态以响应空闲超时、系统活动更改、用户请求或电池过期 ([**IRP \_ MN \_ 设置 \_ power**](./irp-mn-set-power.md)) 

-   查询设备以确定系统是否可以进入睡眠状态 ([**IRP \_ MN \_ query \_ POWER**](./irp-mn-query-power.md)) 

-   若要在查询之后重申当前系统电源状态 (**IRP \_ MN \_ 设置 \_ power**) 

Power manager 发送 **IRP \_ MN \_ QUERY \_ power** 和 IRP MN 代表系统 **\_ \_ 设置 \_ 电源** 请求。 驱动程序可能会失败 **irp \_ MN \_ 查询 \_ 电源** 请求，但不能失败 **irp \_ MN \_ 集的 \_ 电源**。

例如，要更改系统电源状态，电源管理器会将系统电源 IRP 发送到设备树的每个设备节点堆栈中的顶部驱动程序。 下图显示了单个设备堆栈中的驱动程序如何处理系统电源 IRP。

![说明系统电源 irp 的路径的示意图](images/s2dirp.png)

如上图所示：

1.  电源管理器会调用 i/o 管理器，将系统电源 IRP 发送到设备树中的每个叶节点。

2.  驱动程序会在可能的情况下处理 IRP，如有必要，设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，并调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (Windows 7 和 Windows Vista) 或 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (windows Server 2003、windows XP 和 windows 2000) 以将 IRP 向下移动。 如果驱动程序必须使 IRP 失败，则驱动程序将立即执行操作并完成 IRP。 驱动程序可能会失败 **irp \_ MN \_ 查询 \_ 电源** Irp，但不得失败 **irp \_ MN \_ 设置 \_ 电源** irp 来设置系统电源状态。

3.  当拥有设备电源策略的驱动程序收到 IRP 时，该驱动程序将为系统 IRP 设置 *IoCompletion* 例程，然后将 IRP 转发。

4.  堆栈中的任何其他驱动程序会在可能的情况下处理 IRP，如有必要，请设置 *IoCompletion* 例程，并将 IRP 转发到下一个较低的驱动程序，如步骤2所示。

5.  最终，总线驱动程序接收并完成系统 IRP。

6.  当驱动程序通过系统 IRP 向下传递到设备堆栈时，i/o 管理器将调用设置为驱动程序的任何 *IoCompletion* 例程。

7.  在其 *IoCompletion* 例程中，设备电源策略所有者调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 来发送设备电源 IRP，并指定对系统 IRP 中系统电源状态有效的设备电源状态。 驱动程序设置在设备电源 IRP 完成时要调用的回调例程。

    如有必要，驱动程序会在其 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的缓存副本中询问 **DeviceState** 成员 (参阅 [报告设备电源功能](reporting-device-power-capabilities.md)) ，以确定哪种设备电源状态对应于 IRP 中的系统电源状态。

8.  设备 IRP 完成并且所有设备 IRP 完成例程均已运行之后，将调用电源策略所有者的回调例程。 在回调例程中，驱动程序将其返回状态复制到系统 IRP。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，回调调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 来启动下一个 power IRP。 但是，在 Windows 7 和 Windows Vista 中，调用 **PoStartNextPowerIrp** 不是必需的，这样的调用不会执行任何电源管理操作。 最后，回调调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成系统 IRP。

有关详细信息，请参阅 [处理系统电源状态请求](handling-system-power-state-requests.md)。

由于某些设备在开机时需要浪涌电流，因此系统中的系统浪涌电源 Irp 会以同步方式进行处理。 一次只能有一个此类 IRP 处于活动状态。 有关详细信息，请参阅 [调用 IoCallDriver 与调用 PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)。

 

