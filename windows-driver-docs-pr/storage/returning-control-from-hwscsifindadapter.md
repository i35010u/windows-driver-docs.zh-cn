---
title: 从 HwScsiFindAdapter 返回控制权
description: 从 HwScsiFindAdapter 返回控制权
ms.assetid: 689eae76-9b5b-438f-bbdc-5ee11c6fe737
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- 返回值 WDK SCSI
- status 值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a72c85b4b0238a72da3a5289039a06a2a4fc59c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842687"
---
# <a name="returning-control-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 返回控制权


## <span id="ddk_returning_control_from_hwscsifindadapter_kg"></span><span id="DDK_RETURNING_CONTROL_FROM_HWSCSIFINDADAPTER_KG"></span>


当旧微型端口驱动程序的[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) **例程返回**control[**时，如果**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)调用*HwScsiFindAdapter*指示微型端口驱动程序无法支持 HBA。 否则， **ScsiPortInitialize**会声明注册表中的资源，并代表微型端口驱动程序设置必要的系统资源，例如中断和适配器对象。 然后，它会调用微型端口驱动程序的*HwScsiInitialize*例程，如[SCSI 微型端口驱动程序的 HwScsiInitialize 例程](scsi-miniport-driver-s-hwscsiinitialize-routine.md)中所述。

当即插即用微型端口驱动程序的*HwScsiFindAdapter*例程返回控制时，如果调用*HwScsiFindAdapter*指示微型端口驱动程序无法支持 HBA，则允许即插即用管理器卸载微型端口驱动程序. 否则，端口驱动程序将连接中断（在*HwScsiFindAdapter*调用之前已声明并设置的其他资源），并调用微型端口驱动程序的[*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))例程，该例程初始化 HBA。

目前，除了在[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)中设置的值，端口驱动程序还会检查注册表中是否存在禁用下列任一项或全部内容的用户集值：

-   HBA 上的同步传输

    端口驱动程序 Or 为带有 SRB\_标志的 HBA 维护的默认**SrbFlags** ，\_禁用\_同步\_传输。

-   在 HBA 上进行总线断开连接操作

    端口驱动程序 Or 具有 SRB\_标志的默认**SrbFlags**\_禁用\_断开连接。

-   标记的队列

    端口驱动程序将为 HBA 维护的**TaggedQueuing**布尔值设置为**FALSE**。

-   HBA 上请求的内部排队

    端口驱动程序将其维护的**MultipleRequestPerLu**布尔值设置为**FALSE** 。

注册表中紧前面的任何 "disable" 值都将覆盖\_配置\_信息缓冲区的端口中的任何*HwScsiFindAdapter*例程集。 请注意，暂时禁用同步传输、总线断开连接操作、标记排队和 HBA 内部请求队列可以简化使用调试器在正在开发的微型端口驱动程序中跟踪请求处理的操作。

另请注意，基于 NT 的操作系统端口驱动程序使用端口\_配置中的值\_微型端口驱动程序的*HwScsiFindAdapter*例程或其他源（如旧微型端口的注册表）提供的信息驱动程序）以填充存储类驱动程序使用的 IO\_SCSI\_功能数据，如[存储类驱动程序](storage-class-drivers.md)中所述。

 

 




