---
title: SCSI 端口驱动程序的队列管理
description: SCSI 端口驱动程序的队列管理
ms.assetid: ddcbd016-8d8b-4bbc-9c71-b7a5eaa61205
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d1a53c7085d316aa659a26aee4dc43accaa222
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524267"
---
# <a name="scsi-port-drivers-queue-management"></a>SCSI 端口驱动程序的队列管理


## <span id="ddk_scsi_port_driver_s_queue_management_kg"></span><span id="DDK_SCSI_PORT_DRIVER_S_QUEUE_MANAGEMENT_KG"></span>


SCSI 主机适配器可以处理的 I/O 请求在卷中会有很大。 为了避免庞大的任何特定的主机适配器的功能，必须能够控制流的 I/O 请求的存储类驱动程序或存储端口驱动程序。

在 Microsoft Windows 存储体系结构中，SCSI 端口驱动程序处理 I/O 流控制的大多数的方面。 存储类驱动程序可以因此转发任意数量的输入/输出请求到 SCSI 端口进行测试的特定适配器的限制。 SCSI 端口还接受来自存储类驱动程序的显式请求可以暂停队列处理。

SCSI 端口驱动程序称为"冻结"其 I/O 请求队列时它会停止响应的基础硬件报告的错误条件的排队请求的处理。 SCSI 端口称为"锁定"其 I/O 请求队列时它会停止响应的显式请求来自类驱动程序或某些其他更高级别的驱动程序中的处理。

以下部分介绍导致 SCSI 端口以将其队列的状态更改的条件。 它们还描述 Srb 更高级别的驱动程序可以用来对 SCSI 端口的内部 I/O 请求队列进行控制。

 

 




