---
title: SRB\_指示\_主\_时钟
description: SRB\_指示\_主\_时钟
ms.assetid: 76ce59d2-d33c-4cec-a90e-563a16dc476b
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
ms.openlocfilehash: e377c1e965b353e492539dea5add295351f38715
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843300"
---
# <a name="srb_indicate_master_clock"></a>SRB\_指示\_主\_时钟


## <span id="ddk_srb_indicate_master_clock_ks"></span><span id="DDK_SRB_INDICATE_MASTER_CLOCK_KS"></span>


类驱动程序发出此请求，以便向流式传递现在作为其主时钟的时钟对象的句柄，或指示流可自由运行的零句柄。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

类驱动程序设置**CommandData**。*PSrb*指向表示主时钟的时钟对象的句柄的**MasterClockHandle**成员。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

流可以通过将主时钟句柄传递到[**StreamClassQueryMasterClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassquerymasterclock)或[**StreamClassQueryMasterClockSync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassquerymasterclocksync)来查询主时钟的时间值。

在微型驱动程序收到 SRB\_指示特定流\_主\_时钟之前，它可能会假设流可以自由运行。 如果此 SRB 中为从属 pin 传递的句柄与在 SRB 中传递给微型驱动程序的句柄相同（ [ **\_打开\_MASTER\_时钟**](srb-open-master-clock.md)），则微型驱动程序可以直接从主时钟读取时间，因为它控制主时钟和从属。

微型驱动程序应保留 SRB 中的**MasterClockHandle**字段，该字段指向主时钟的句柄。 如果此句柄为零，则表示微型驱动程序此流现在可以自由运行，不能从属于主时钟。

 

 





