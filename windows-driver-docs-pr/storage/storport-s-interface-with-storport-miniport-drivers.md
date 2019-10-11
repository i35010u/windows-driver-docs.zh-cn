---
title: Storport 与 Storport 微型端口驱动程序的接口
description: Storport 与 Storport 微型端口驱动程序的接口
ms.assetid: 8e09d6a6-7e4f-44fc-a2b0-5f21b4ac0593
ms.date: 06/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: ce25d0b6b39cc928f0c1dde7ceaaca868a783a4f
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252395"
---
# <a name="storports-interface-with-storport-miniport-drivers"></a>Storport 与 Storport 微型端口驱动程序的接口

Storport 驱动程序和 Storport 微型端口驱动程序之间的通信是通过 SCSI 请求块（SRBs）和微型端口驱动程序回调例程来进行的。 有关 Storport 微型端口驱动程序回调例程的详细讨论，请参阅[Storport 微型端口驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-driver-routines)。

有关各个 SRB 函数、SRB 标志和 SRB 状态值的概述和定义，请参阅[**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)。

有关微型端口驱动程序必须如何响应每个单独的 SRB 函数的讨论，请参阅[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)。

Storport 将 SRBs 转发到用于异步处理的 Storport 微型端口驱动程序。 通常，微型端口驱动程序将需要一段时间才能真正完成该请求。 支持标记队列的主机总线适配器（Hba）可以在内部对请求进行排队，并按 Storport 分配给每个请求的标记指示的顺序进行处理。 [**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio) （SRB）结构包含以下两个成员： Storport 和微型端口驱动程序使用它来指定如何在主机适配器的内部队列中对 SRBs 进行排序：

* **QueueTag**：Storport 向每个 SRB 的**QueuedTag**成员分配一个计数或 *"标记"* 值。 此标记指示适配器处理数据包的顺序。 标记值还允许 Storport 跟踪哪些 SRBs 仍未完成，哪些已成功完成，哪些已超时。

* **QueueAction**：指示在 SRB 中设置 SRB_FLAGS_QUEUE_ACTION_ENABLE 标志时要使用的标记排队消息 **。SrbFlags**。 小型端口使用**QueueAction**是特定于微型端口的。 如果 HBA 支持基于 SCSI 的微型端口，则可以遵循 SCSI 规范。 **QueueAction**可以是下列值之一：

| ReplTest1 | 含义 |
| ----- | ------- |
| SRB_SIMPLE_TAG_REQUEST | 将请求排队，并在所有较早的 SRB_HEAD_OF_QUEUE_TAG_REQUEST 和 SRB_ORDERED_QUEUE_TAG_REQUEST 请求结束后按任意顺序执行。 |
| SRB_ORDERED_QUEUE_TAG_REQUEST | 仅在所有较早的 SRB_HEAD_OF_QUEUE_TAG_REQUEST 和所有旧的请求完成后执行请求。 |
| SRB_HEAD_OF_QUEUE_TAG_REQUEST | 将请求放在队列的前面，并在队列中的所有其他请求之前执行该请求，包括所有其他 SRB_HEAD_OF_QUEUE_TAG_REQUEST 标记的请求。 |

有关详细信息，请参阅 SCSI 规范。