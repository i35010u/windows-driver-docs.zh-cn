---
title: ATA 端口驱动程序的队列管理
description: ATA 端口驱动程序的队列管理
ms.assetid: feba86a6-2b89-41c9-9b14-b76c2522a332
keywords:
- ATA 端口驱动程序 WDK，队列
- 队列 WDK ATA 端口驱动程序
- 设备队列 WDK ATA 端口驱动程序
- LUN 队列 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec23706d25cf5c60853b470f5ff39f5b21a4dda0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368425"
---
# <a name="ata-port-drivers-queue-management"></a>ATA 端口驱动程序的队列管理


## <span id="ddk_ata_port_drivers_queue_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_QUEUE_MANAGEMENT_KG"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


ATA 端口驱动程序维护的微型端口驱动程序公开每个逻辑单元号 (LUN) 的设备队列和每个通道的 IDE 控制器上启用的单独的队列。 这些队列协同工作来控制对微型端口驱动程序的请求的流。

下图显示了如何请求流入从端口驱动程序的 LUN 队列通道队列。

![ata 设备和通道队列](images/ataqueues.png)

由于 ATA 端口驱动程序使用推送模型的 I/O，ATA 端口驱动程序不会等待微型端口驱动程序，它将转发到微型端口驱动程序的下一个数据包之前请求输入。 有关 ATA 端口驱动程序使用的 I/O 模型的信息，请参阅[ATA 端口 I/O 模型](ata-port-i-o-model.md)。

不过，ATA 端口驱动程序*does*限制它会向下推送到微型端口驱动程序的请求数。 请求数是微型端口驱动程序将分配给的值**NumberOfOverlappedRequests**的成员[ **IDE\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_channel_configuration)结构。 ATA 端口驱动程序会维护它已转发给给定通道及其微型端口驱动程序的未完成"重叠"请求数的计数。 如果此数值超出了中的值**NumberOfOverlappedRequests**，ATA 端口驱动程序将停止将新的请求传递给微型端口驱动程序。 ATA 端口驱动程序在其队列中保留的所有新请求，并等待要完成某些请求的微型端口驱动程序。 未完成的请求数低于中的值后**NumberOfOverlappedRequests**，端口驱动程序恢复将请求发送到微型端口驱动程序。

ATA 微型端口驱动程序还可以控制通过调用从端口驱动程序收到的请求流[ **AtaPortDeviceBusy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportdevicebusy)并[ **AtaPortDeviceReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportdeviceready)例程。

 

 


