---
title: 从 HwScsiFindAdapter 返回控制权
description: 从 HwScsiFindAdapter 返回控制权
ms.assetid: 689eae76-9b5b-438f-bbdc-5ee11c6fe737
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
- 返回值 WDK SCSI
- 状态值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cda7f2b37b80c9ed48bc4e0791f986a3583bd8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386116"
---
# <a name="returning-control-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 返回控制权


## <span id="ddk_returning_control_from_hwscsifindadapter_kg"></span><span id="DDK_RETURNING_CONTROL_FROM_HWSCSIFINDADAPTER_KG"></span>


当旧的微型端口驱动程序的[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程将返回控件[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)返回到**DriverEntry**日常如果到拜访*HwScsiFindAdapter*指示微型端口驱动程序不支持 HBA。 否则为**ScsiPortInitialize**声明注册表中的资源，并设置必要的系统资源，例如中断和适配器对象，代表微型端口驱动程序。 然后，它将调用微型端口驱动程序*HwScsiInitialize*例程中所述[SCSI 微型端口驱动程序 HwScsiInitialize 例程](scsi-miniport-driver-s-hwscsiinitialize-routine.md)。

当插微型端口驱动程序的*HwScsiFindAdapter*例程返回控制，允许插管理器卸载微型端口驱动程序，如果到拜访*HwScsiFindAdapter*指示微型端口驱动程序不支持 HBA。 否则，端口驱动程序连接中断 (已声明并之前设置了其他资源*HwScsiFindAdapter*调用)，并调用微型端口驱动程序[ *HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))例程，初始化 HBA。

目前，除了值设置[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)，端口驱动程序还会检查任何禁用的用户设置值的注册表或将以下所有：

-   HBA 上同步传输

    端口驱动程序 Or 默认**SrbFlags**它为与 SRB HBA 维护\_标志\_禁用\_同步\_传输。

-   HBA 上的总线断开连接操作

    端口驱动程序 Or 默认**SrbFlags**与 SRB\_标志\_禁用\_断开连接。

-   有标记的队列

    端口驱动程序集**TaggedQueuing**布尔值，它还为到 HBA 保留**FALSE**。

-   HBA 上请求的内部队列

    端口驱动程序将设置为**FALSE** **MultipleRequestPerLu**布尔值，它会维护有关 HBA。

任何在注册表中的前面紧邻"禁用"值将覆盖任何*HwScsiFindAdapter*在端口中设置例程\_配置\_信息缓冲区。 请注意，暂时禁用同步传输总线-断开连接操作、 有标记的队列和 HBA 内部请求队列可以简化使用跟踪请求处理正在开发的微型端口驱动程序中的调试器。

基于 NT 的操作系统端口驱动程序，从端口使用的值另请注意\_配置\_提供的微型端口驱动程序的信息*HwScsiFindAdapter*例程或从其他源 （如旧的微型端口驱动程序的注册表） 的 IO 中填满\_SCSI\_功能数据以供存储类驱动程序，如中所述[存储类驱动程序](storage-class-drivers.md)。

 

 




