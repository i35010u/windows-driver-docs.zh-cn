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
ms.openlocfilehash: f53e19e772ccf720f84c4eea112a6eecc4cc147a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845106"
---
# <a name="ata-port-drivers-queue-management"></a>ATA 端口驱动程序的队列管理


## <span id="ddk_ata_port_drivers_queue_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_QUEUE_MANAGEMENT_KG"></span>


**注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用[storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)程序和[storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


ATA 端口驱动程序为每个逻辑单元号（LUN）维护一个设备队列，每个逻辑单元号（LUN）由微型端口驱动程序公开，并为 IDE 控制器上启用的每个通道单独提供一个队列。 这些队列一起工作以控制发送到微型端口驱动程序的请求流。

下图显示了请求如何从端口驱动程序的 LUN 队列流向通道队列。

![ata 设备和通道队列](images/ataqueues.png)

因为 ATA 端口驱动程序使用 i/o 推送模式，所以 ATA 端口驱动程序不会等待微型端口驱动程序请求输入，然后再将下一个数据包转发到微型端口驱动程序。 有关 ATA 端口驱动程序使用的 i/o 模型的信息，请参阅[Ata 端口 I/o 型号](ata-port-i-o-model.md)。

尽管如此，ATA 端口驱动程序也*会*限制向下推送到微型端口驱动程序的请求数。 请求数是微型端口驱动程序为[**IDE\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/ns-irb-_ide_channel_configuration)结构分配给**NumberOfOverlappedRequests**成员的值。 ATA 端口驱动程序维护已为给定通道转发到其微型端口驱动程序的未完成 "重叠" 请求数的计数。 如果此数字超出**NumberOfOverlappedRequests**中的值，则 ATA 端口驱动程序会停止将新请求传递到微型端口驱动程序。 ATA 端口驱动程序会在其队列中保留所有新请求，并等待微型端口驱动程序完成某些请求。 当未完成的请求数降到**NumberOfOverlappedRequests**中的值以下后，端口驱动程序将恢复向微型端口驱动程序发送请求。

ATA 微型端口驱动程序还可以通过调用[**AtaPortDeviceBusy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportdevicebusy)和[**AtaPortDeviceReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportdeviceready)例程来控制它从端口驱动程序接收的请求流。

 

 


