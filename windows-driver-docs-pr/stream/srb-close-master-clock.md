---
title: SRB\_关闭\_MASTER\_时钟
description: SRB\_关闭\_MASTER\_时钟
ms.assetid: 5d49f64a-22e0-4fec-a9f5-4ce5169fa305
keywords:
- SRB_CLOSE_MASTER_CLOCK 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467ff76acb23c0f4a180249d644166c1e2447fd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365205"
---
# <a name="srbclosemasterclock"></a>SRB\_关闭\_MASTER\_时钟


## <span id="ddk_srb_close_master_clock_ks"></span><span id="DDK_SRB_CLOSE_MASTER_CLOCK_KS"></span>


在类驱动程序发出此请求，以指示流，它不再微型驱动程序的主时钟。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

 

 





