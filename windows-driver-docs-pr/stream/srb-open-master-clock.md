---
title: SRB\_开放\_MASTER\_时钟
description: SRB\_开放\_MASTER\_时钟
ms.assetid: 1ccad1bc-27e7-4038-b341-389240051fb8
keywords:
- SRB_OPEN_MASTER_CLOCK 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_OPEN_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa3b353712b3d3c2ac6537df22866bab13c8738b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387075"
---
# <a name="srbopenmasterclock"></a>SRB\_开放\_MASTER\_时钟


## <span id="ddk_srb_open_master_clock_ks"></span><span id="DDK_SRB_OPEN_MASTER_CLOCK_KS"></span>


在类驱动程序发出此请求，以指示流，它现在充当主时钟的微型驱动程序。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

类驱动程序集**CommandData**。**MasterClockHandle**指向成员*pSrb*时钟对象的句柄到它创建表示主时钟。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。

微型驱动程序应保留**CommandData.MasterClockHandle**字段指向主时钟的句柄 SRB 中的值。

 

 





