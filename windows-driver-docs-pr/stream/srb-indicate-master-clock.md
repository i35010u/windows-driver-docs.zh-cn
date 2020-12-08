---
title: SRB \_ 表示 \_ 主 \_ 时钟
description: SRB \_ 表示 \_ 主 \_ 时钟
keywords:
- SRB_INDICATE_MASTER_CLOCK 流媒体设备
topic_type:
- apiref
api_name:
- SRB_INDICATE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ddcd14f3ec17afcfc99bee08d993fcad6e914d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840499"
---
# <a name="srb_indicate_master_clock"></a>SRB \_ 表示 \_ 主 \_ 时钟


## <span id="ddk_srb_indicate_master_clock_ks"></span><span id="DDK_SRB_INDICATE_MASTER_CLOCK_KS"></span>


类驱动程序发出此请求，以便向流式传递现在作为其主时钟的时钟对象的句柄，或指示流可自由运行的零句柄。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>注释

类驱动程序设置 **CommandData**。*PSrb* 指向表示主时钟的时钟对象的句柄的 **MasterClockHandle** 成员。 *PSrb* 指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

流可以通过将主时钟句柄传递到 [**StreamClassQueryMasterClock**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassquerymasterclock) 或 [**StreamClassQueryMasterClockSync**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassquerymasterclocksync)来查询主时钟的时间值。

在微型驱动程序收到 SRB \_ 指示 \_ \_ 特定流的主时钟之前，它可能会假设流可以自由运行。 如果此 SRB 中为从属 pin 传递的句柄与在 [**SRB \_ OPEN \_ master \_ 时钟**](srb-open-master-clock.md)中传递给微型驱动程序的句柄相同，则微型驱动程序可以直接从主时钟读取时间，因为它控制主时钟和从属项。

微型驱动程序应保留 SRB 中的 **MasterClockHandle** 字段，该字段指向主时钟的句柄。 如果此句柄为零，则表示微型驱动程序此流现在可以自由运行，不能从属于主时钟。

 

