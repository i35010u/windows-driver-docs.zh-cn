---
title: SRB\_打开\_母版\_时钟
description: SRB\_打开\_母版\_时钟
ms.assetid: 1ccad1bc-27e7-4038-b341-389240051fb8
keywords:
- SRB_OPEN_MASTER_CLOCK 流媒体设备
topic_type:
- apiref
api_name:
- SRB_OPEN_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbc9301aa626f81007b21ecf68064e5661d34ba9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843291"
---
# <a name="srb_open_master_clock"></a>SRB\_打开\_母版\_时钟


## <span id="ddk_srb_open_master_clock_ks"></span><span id="DDK_SRB_OPEN_MASTER_CLOCK_KS"></span>


类驱动程序发出此请求，以向流表明它现在作为微型驱动程序的主时钟。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>成功\_状态  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_未\_实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>IO\_设备状态\_\_错误  
指示出现硬件故障。

### <a name="comments"></a>备注

类驱动程序设置**CommandData**。*PSrb*的**MasterClockHandle**成员指向其创建用于表示主时钟的时钟对象的句柄。 *PSrb*指针指向[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。

微型驱动程序应将 SRB 中的**MasterClockHandle**字段值保留到主时钟的句柄。

 

 





