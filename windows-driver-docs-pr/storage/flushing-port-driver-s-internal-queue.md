---
title: 刷新端口驱动程序的内部队列
description: 刷新端口驱动程序的内部队列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42461d2d657cf0486e521ca9cb30146b2213212b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804609"
---
# <a name="flushing-port-drivers-internal-queue"></a>刷新端口驱动程序的内部队列


## <span id="ddk_flushing_port_driver_s_internal_queue_kg"></span><span id="DDK_FLUSHING_PORT_DRIVER_S_INTERNAL_QUEUE_KG"></span>


SCSI 端口驱动程序支持刷新请求，这允许更高级别的驱动程序刷新在内部缓存数据的设备和适配器的缓存。 为了保持数据完整性，应在关闭系统之前刷新所有内部缓存。 接收刷新请求时，SCSI 端口还会刷新其自己的内部队列，并取消所有排队的请求。

更高级别的驱动程序可以通过 \_ \_ \_ 向 SCSI 端口驱动程序发送 SRB 类型的 SRB，来刷新主机适配器的缓存和 scsi 端口的内部队列。 接收到此 SRB 后，SCSI 端口会刷新主机适配器缓存，然后完成其内部队列中的所有请求，并将其 **SrbStatus** 成员设置为刷新的 SRB \_ 状态 \_ 请求 \_ 。 如果 SCSI 端口的队列已冻结， \_ 则 SRB FUNCTION \_ FLUSH queue 会对队列进行 \_ 解冻的副作用。

有关存储微型端口驱动程序如何处理刷新请求的讨论，请参阅 [处理 SRB \_ 函数 \_ flush 和 SRB \_ 函数 \_ 关闭](handling-srb-function-flush-and-srb-function-shutdown.md)。

 

 




