---
title: ATA 端口 I/O 模型中的同步
description: ATA 端口 I/O 模型中的同步
ms.assetid: 91b95588-8cf7-4833-84c2-a991fd066fb2
keywords:
- ATA 端口驱动程序 WDK，同步
- 同步 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91d62a16f94d32fec7c25a1d2ba239ded2e38a54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368168"
---
# <a name="synchronization-in-the-ata-port-io-model"></a>ATA 端口 I/O 模型中的同步


## <span id="ddk_synchronization_in_the_ata_port_i_o_model_kg"></span><span id="DDK_SYNCHRONIZATION_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


ATA 端口驱动程序可以配置为同步对关键数据结构，例如设备扩展的访问由 ATA 微型端口驱动程序例程。 它是由其他微型端口驱动程序例程，访问与同步访问中断处理程序尤其重要，因为这些访问可能会出现在不同的线程上下文中。

ATA 端口驱动程序可以在两种同步模式之一运行。 一种模式中的微型端口驱动程序与中断服务例程进行同步。 在另一种模式中它不会同步。 ATA 微型端口驱动程序可以通过设置指定同步模式**SyncWithIsr**的成员[ **IDE\_通道\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_channel_configuration)结构。 如果微型端口驱动程序设置**SyncWithIsr**到**TRUE**，ATA 端口驱动程序引发到 DIRQL IRQL 之前它将调用任意以下微型端口驱动程序例程：[**IdeHwInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_initialize)， [ **IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_startio)，或者[ **IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_reset)。 下表指示的值分配给**SyncWithIsr**影响 IRQL 的 ATA 端口驱动程序调用 ATA 微型端口驱动程序例程。

**通道接口中的微型端口驱动程序例程**

**IRQL**

**SyncWithIsr = TRUE**

**SyncWithIsr = FALSE**

***AtaChannelInitRoutine***

被动\_级别

被动\_级别

***IdeHwControl***

(使用参数 ControlAction = StartChannel)

被动\_级别

被动\_级别

***IdeHwControl***

(使用参数 ControlAction = StopChannel)

被动\_级别

被动\_级别

***IdeHwControl***

(使用参数 ControlAction = PowerUpChannel)

&lt;= DISPATCH\_LEVEL

&lt;= DISPATCH\_LEVEL

***IdeHwControl***

(使用参数 ControlAction = PowerDownChannel)

&lt;= DISPATCH\_LEVEL

&lt;= DISPATCH\_LEVEL

***IdeHwBuildIo***

&lt;= DISPATCH\_LEVEL

&lt;= DISPATCH\_LEVEL

辅助角色例程 （回调）

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

同步例程 (由指定的回调例程[ **AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestsynchronizedroutine))

DIRQL

DIRQL

***IdeHwInterrupt***

DIRQL

DIRQL

 

即使**SyncWithIsr**设置为**FALSE**，微型端口驱动程序可以通过调用与中断处理程序同步的回调例程[ **AtaPortRequestSynchronizedRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestsynchronizedroutine)和它将指针传递到回调例程。

同步是基于每个通道。 因此上一个同步通道，, 没有两个微型端口驱动程序例程将执行一次，但在单独的同步通道上运行的例程可并发执行。

 

 


