---
title: ATA 端口 I/O 模型中的同步
description: ATA 端口 I/O 模型中的同步
ms.assetid: 91b95588-8cf7-4833-84c2-a991fd066fb2
keywords:
- ATA 端口驱动程序 WDK，同步
- 同步 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e46f0f6eea97d3a0a2814ab9f0d31f101243ea2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844454"
---
# <a name="synchronization-in-the-ata-port-io-model"></a>ATA 端口 I/O 模型中的同步


## <span id="ddk_synchronization_in_the_ata_port_i_o_model_kg"></span><span id="DDK_SYNCHRONIZATION_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>


**注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用[storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)程序和[storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


ATA 端口驱动程序可以配置为通过 ATA 微型端口驱动程序例程来同步对关键数据结构（例如设备扩展）的访问。 中断处理程序的访问与其他微型端口驱动程序例程的访问是同步的，因为这些访问可能发生在不同的线程上下文中。

ATA 端口驱动程序可以在两种同步模式中运行。 在一种模式下，微型端口驱动程序与中断服务例程同步。 在其他模式下，它不会同步。 ATA 微型端口驱动程序可以通过设置[**IDE\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/ns-irb-_ide_channel_configuration)结构的**SyncWithIsr**成员来指定同步模式。 如果微型端口驱动程序将**SyncWithIsr**设置为**TRUE**，则 ATA 端口驱动程序会在调用以下任意微型端口驱动程序例程之前，将 IRQL 提升为 DIRQL： [**IdeHwInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_initialize)、 [**IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_startio)或[**IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_reset)。 下表指示分配给**SyncWithIsr**的值如何影响 ata 端口驱动程序调用 ata 微型端口驱动程序例程的 IRQL。

**通道接口中的微型端口驱动程序例程**

**IRQL**

**SyncWithIsr = TRUE**

**SyncWithIsr = FALSE**

***AtaChannelInitRoutine***

被动\_级别

被动\_级别

***IdeHwControl***

（参数 ControlAction = StartChannel）

被动\_级别

被动\_级别

***IdeHwControl***

（参数 ControlAction = StopChannel）

被动\_级别

被动\_级别

***IdeHwControl***

（参数 ControlAction = PowerUpChannel）

&lt;= 调度\_级别

&lt;= 调度\_级别

***IdeHwControl***

（参数 ControlAction = PowerDownChannel）

&lt;= 调度\_级别

&lt;= 调度\_级别

***IdeHwBuildIo***

&lt;= 调度\_级别

&lt;= 调度\_级别

辅助例程（回调）

调度\_级别

调度\_级别

***IdeHwInitialize***

DIRQL

调度\_级别

***IdeHwStartIo***

DIRQL

调度\_级别

***IdeHwReset***

DIRQL

调度\_级别

同步例程（ [**AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestsynchronizedroutine)指定的回调例程）

DIRQL

DIRQL

***IdeHwInterrupt***

DIRQL

DIRQL

 

即使**SyncWithIsr**设置为**FALSE**，微型端口驱动程序也可以通过调用[**AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestsynchronizedroutine)并向其传递一个指向回调例程的指针，来将回调例程与中断处理程序同步。

同步基于每个通道。 因此，在同步通道上，不会同时执行两个小型端口驱动程序例程，而在单独的同步通道上运行的例程可以并发执行。

 

 


