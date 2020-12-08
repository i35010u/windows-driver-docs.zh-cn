---
title: 从 HwScsiFindAdapter 调用 ScsiPortXxx
description: 从 HwScsiFindAdapter 调用 ScsiPortXxx
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- 调用 ScsiPortXxx 例程 WDK 存储
- ScsiPortXxx 调用
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: f4a78350ede00d577d0b281f9a3cfd70d9e16ec5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811775"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 调用 ScsiPortXxx

某些 **ScsiPort**_Xxx_ 例程 *只能从微型* 端口驱动程序的 *HwScsiFindAdapter*)  (例程调用，具体如下所示：

- [**ScsiPortValidateRange**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportvalidaterange) 验证是否尚未在注册表中通过另一台设备的驱动程序来声明微型端口驱动程序提供的总线相关访问范围。

- [**ScsiPortGetDeviceBase**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase) 用于将 HBA 的 (总线相关) "物理" 地址范围映射到系统分配的逻辑地址范围，该范围由驱动程序通过使用映射的逻辑范围地址调用 **ScsiPortRead**_xxx_ 和 **ScsiPortWrite**_Xxx_ 例程来与 hba 通信。

- 如果 *HwScsiFindAdapter* 在给定 i/o 总线上找不到可支持的 HBA （如端口 [**ScsiPortFreeDeviceBase**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportfreedevicebase) \_ 配置 \_ 信息 **SystemIoBusNumber** 值所示），则 ScsiPortFreeDeviceBase 释放此类映射范围。

- [**ScsiPortGetUncachedExtension**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetuncachedextension) 分配系统和总线主机 HBA 之间共享的 DMA 缓冲区。

除了这四个例程以外，还有一个例程只能从微型端口驱动程序的 *HwScsiFindAdapter* 例程调用，*或* 在控件类型为 **ScsiSetRunningConfig** 时从 *HwScsiAdapterControl* 调用：

- [**ScsiPortGetBusData**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetbusdata) 获取 BUS_DATA_TYPE 特定的配置信息，如总线相关设备内存 (访问) 范围、中断矢量或 IRQL 以及 DMA 通道或端口。

有关这些 **ScsiPort**_Xxx_ 例程的详细信息，请参阅 [SCSI 端口驱动程序支持例程](scsi-port-driver-support-routines.md)。
