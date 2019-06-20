---
title: Storport 的接口与 Storport 微型端口驱动程序
description: Storport 的接口与 Storport 微型端口驱动程序
ms.assetid: 8e09d6a6-7e4f-44fc-a2b0-5f21b4ac0593
ms.date: 06/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7b94d8738922399f4fb7f13c020264f758aad05c
ms.sourcegitcommit: d5e42ba5e760f3f993007c698a0169a893a81546
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67253360"
---
# <a name="storports-interface-with-storport-miniport-drivers"></a>Storport 的接口与 Storport 微型端口驱动程序

之间的通信 Storport 驱动程序和 Storport 微型端口驱动程序都通过 SCSI 请求块 (Srb) 和微型端口驱动程序回调例程。 Storport 微型端口驱动程序回调例程的详细讨论，请参阅[Storport 驱动程序微型端口例程](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver-miniport-routines)。

有关概述，以及各个 SRB 函数、 SRB 标志和 SRB 状态值的定义，请参阅[ **SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)。

有关如何微型端口驱动程序必须应对每个 SRB 函数的讨论，请参阅[ **HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)。

Storport 将 Srb 转发到 Storport 微型端口驱动程序以进行异步处理。 通常情况下，微型端口驱动程序将需要一些时间来实际完成该请求。 主机总线适配器 (Hba) 支持有标记的队列的可以在内部对请求进行排队，并指示由标记 Storport 分配到每个请求的顺序处理它们。 [ **SCSI_REQUEST_BLOCK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio) (SRB) 结构中包含的 Storport 和微型端口驱动程序使用来指定 Srb 主机适配器的内部队列中的排序方式的两个成员：

* **QueueTag**:Storport 分配计数，或 *"标记"* 值，为**QueuedTag**的每个 SRB 成员。 此标记指示适配器应在其中处理的数据包的顺序。 标记值还允许 Storport 跟踪哪些 Srb 仍未完成，其中已成功完成，以及已超时。

* **QueueAction**： 指示标记队列消息中设置了 SRB_FLAGS_QUEUE_ACTION_ENABLE 标志时要使用**SRB。SrbFlags**。 微型端口用法**QueueAction**是特定于微型端口的。 在基于 SCSI 的微型端口可以按照 SCSI 规范，如果 HBA 支持它。 **QueueAction**可以是下列值之一：

| ReplTest1 | 含义 |
| ----- | ------- |
| SRB_SIMPLE_TAG_REQUEST | 对请求进行排队和所有较旧的 SRB_HEAD_OF_QUEUE_TAG_REQUEST 和 SRB_ORDERED_QUEUE_TAG_REQUEST 请求已结束后，按任意顺序执行它。 |
| SRB_ORDERED_QUEUE_TAG_REQUEST | 仅在完成所有旧 SRB_HEAD_OF_QUEUE_TAG_REQUEST 和较旧的所有请求后，请执行请求。 |
| SRB_HEAD_OF_QUEUE_TAG_REQUEST | 将请求放在前面的队列，并包括所有其他 SRB_HEAD_OF_QUEUE_TAG_REQUEST 标记请求队列中的所有其他请求之前执行它。 |

请参阅详细信息的 SCSI 规范。