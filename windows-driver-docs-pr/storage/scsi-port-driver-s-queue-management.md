---
title: SCSI 端口驱动程序的队列管理
description: SCSI 端口驱动程序的队列管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3c36bd39522bc85f444315c9d98fe42b7237d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805999"
---
# <a name="scsi-port-drivers-queue-management"></a>SCSI 端口驱动程序的队列管理


## <span id="ddk_scsi_port_driver_s_queue_management_kg"></span><span id="DDK_SCSI_PORT_DRIVER_S_QUEUE_MANAGEMENT_KG"></span>


SCSI 主机适配器可处理的 i/o 请求量大不相同。 为了避免任何特定主机适配器的功能，存储类驱动程序或存储端口驱动程序必须能够控制 i/o 请求的流动。

在 Microsoft Windows 存储体系结构中，SCSI 端口驱动程序处理 i/o 流控制的大多数方面。 因此，存储类驱动程序可以将任意数量的 i/o 请求转发到 SCSI 端口，而不测试特定适配器的限制。 SCSI 端口还接受来自存储类驱动程序的显式请求，以暂停队列处理。

SCSI 端口驱动程序将在每次暂停处理排队请求时 "冻结" 其 i/o 请求队列，以响应基础硬件报告的错误条件。 SCSI 端口被称为 "锁定" 其 i/o 请求队列，这是因为它在响应来自类驱动程序或其他更高级别驱动程序的显式请求时暂停处理。

以下部分介绍导致 SCSI 端口更改其队列状态的条件。 它们还介绍了更高级别的驱动程序可以使用的 SRBs，以控制 SCSI 端口的内部 i/o 请求队列。

 

 




