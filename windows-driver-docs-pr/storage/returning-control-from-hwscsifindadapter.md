---
title: 从 HwScsiFindAdapter 返回控制权
description: 从 HwScsiFindAdapter 返回控制权
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- 返回值 WDK SCSI
- status 值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3bf345c20e17368d91240f410ae52e1307f390c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802201"
---
# <a name="returning-control-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 返回控制权

当旧微型端口驱动程序的 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程返回 control 时，如果调用 (s) 为 *HwScsiFindAdapter* ，则 [**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)返回 **DriverEntry** 例程，指示微型端口驱动程序无法支持 HBA。 否则， **ScsiPortInitialize** 会声明注册表中的资源，并代表微型端口驱动程序设置必要的系统资源，例如中断和适配器对象。 然后，它会调用微型端口驱动程序的 *HwScsiInitialize* 例程，如 [SCSI 微型端口驱动程序的 HwScsiInitialize 例程](scsi-miniport-driver-s-hwscsiinitialize-routine.md)中所述。

如果即插即用微型端口驱动程序的 *HwScsiFindAdapter* 例程返回控制权，则允许即插即用 manager 卸载微型端口驱动程序，前提是调用 (s) 为 *HwScsiFindAdapter* 指示微型端口驱动程序无法支持 HBA。 否则，端口驱动程序会将中断连接 (在 *HwScsiFindAdapter* 调用) 之前已经声明和设置的其他资源，并调用微型端口驱动程序的 [*HwScsiInitialize*](/previous-versions/windows/hardware/drivers/ff557302(v=vs.85)) 例程，这会初始化 HBA。

目前，除了在 [PORT_CONFIGURATION_INFORMATION](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)中设置的值，端口驱动程序还会检查注册表中是否存在禁用下列任一项或全部内容的用户集值：

- HBA 上的同步传输：端口驱动程序 Or 为 HBA 提供 SRB_FLAGS_DISABLE_SYNCH_TRANSFER 的默认 **SrbFlags** 。

- 对 HBA 执行的总线断开连接操作：端口驱动程序 Or 默认的 **SrbFlags** SRB_FLAGS_DISABLE_DISCONNECT。

- 标记队列：端口驱动程序将为 HBA 维护的 **TaggedQueuing** 布尔值设置为 **FALSE**。

- HBA 上请求的内部排队：端口驱动程序将其维护的 **MultipleRequestPerLu** 布尔值设置为 **FALSE** 。

注册表中紧前面的任何 "disable" 值都将覆盖 PORT_CONFIGURATION_INFORMATION 缓冲区中的任何 *HwScsiFindAdapter* 例程集。 请注意，暂时禁用同步传输、总线断开连接操作、标记排队和 HBA 内部请求队列可以简化使用调试器在正在开发的微型端口驱动程序中跟踪请求处理的操作。

另请注意，基于 NT 的操作系统端口驱动程序使用微型端口驱动程序的 *HwScsiFindAdapter* 例程提供的 PORT_CONFIGURATION_INFORMATION 中的值，或者使用来自其他源的值 (例如旧版微型端口驱动程序的注册表) ，以填充存储类驱动程序使用的 IO_SCSI_CAPABILITIES 数据，如 [存储类驱动程序](introduction-to-storage-class-drivers.md)中所述。
