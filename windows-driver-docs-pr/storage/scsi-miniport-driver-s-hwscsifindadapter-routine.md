---
title: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
description: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beba4acb740c79df14aa3fff73c74f859205df23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828413"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


操作系统特定的端口驱动程序在配置信息缓冲区中填充的 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) 与端口配置信息的数量一样大，因为它可以从微型端口驱动程序的 [**HW \_ 初始化 \_ 数据中 (SCSI)**](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data) 规范和系统中的其他源，然后再使用指向配置信息缓冲区的指针调用给定的 *HwScsiFindAdapter* 例程。

通常， *HwScsiFindAdapter* 例程负责使用提供的配置信息和/或调用 **ScsiPort**_Xxx_ 来收集足够的配置信息，以确定它是否支持由 **SystemIoBusNumber** \_ \_ 端口驱动程序提供的端口配置信息中的 SystemIoBusNumber 标识的 i/o 总线上的 HBA。 如果是这样，则 *HwScsiFindAdapter* 负责为端口配置信息中的支持的 HBA 填写所有剩余的配置信息 \_ \_ ，以便使用有关该 HBA 的驱动程序确定状态设置微型端口驱动程序的设备扩展，并在返回 control 之前将 *再次* 参数设置为合适的值。

有关详细信息，请参阅 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) 和 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 。

 

