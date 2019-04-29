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
ms.openlocfilehash: 3a987b07a9f153f9c2e063c52f5607525f685aea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391523"
---
# <a name="returning-control-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 返回控制权


## <span id="ddk_returning_control_from_hwscsifindadapter_kg"></span><span id="DDK_RETURNING_CONTROL_FROM_HWSCSIFINDADAPTER_KG"></span>


当旧的微型端口驱动程序的[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)例程将返回控件[ **ScsiPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff564645)返回到**DriverEntry**日常如果到拜访*HwScsiFindAdapter*指示微型端口驱动程序不支持 HBA。 否则为**ScsiPortInitialize**声明注册表中的资源，并设置必要的系统资源，例如中断和适配器对象，代表微型端口驱动程序。 然后，它将调用微型端口驱动程序*HwScsiInitialize*例程中所述[SCSI 微型端口驱动程序 HwScsiInitialize 例程](scsi-miniport-driver-s-hwscsiinitialize-routine.md)。

当插微型端口驱动程序的*HwScsiFindAdapter*例程返回控制，允许插管理器卸载微型端口驱动程序，如果到拜访*HwScsiFindAdapter*指示微型端口驱动程序不支持 HBA。 否则，端口驱动程序连接中断 (已声明并之前设置了其他资源*HwScsiFindAdapter*调用)，并调用微型端口驱动程序[ *HwScsiInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff557302)例程，初始化 HBA。

目前，除了值设置[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)，端口驱动程序还会检查任何禁用的用户设置值的注册表或将以下所有：

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

 

 




