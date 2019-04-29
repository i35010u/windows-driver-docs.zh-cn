---
title: SRB\_指示\_MASTER\_时钟
description: SRB\_指示\_MASTER\_时钟
ms.assetid: 76ce59d2-d33c-4cec-a90e-563a16dc476b
keywords:
- SRB_INDICATE_MASTER_CLOCK 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_INDICATE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f23a17bc8a404ee9fb93809db24ccdc33966272c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390861"
---
# <a name="srbindicatemasterclock"></a>SRB\_指示\_MASTER\_时钟


## <span id="ddk_srb_indicate_master_clock_ks"></span><span id="DDK_SRB_INDICATE_MASTER_CLOCK_KS"></span>


类驱动程序将发出此请求，以指示为流现在可作为其主时钟的时钟对象的句柄或零以指示该流的句柄没有运行。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

类驱动程序集**CommandData**。**MasterClockHandle**指向成员*pSrb*到表示主时钟的时钟对象的句柄。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。

流可能会查询主时钟的时间值表示通过主时钟句柄[ **StreamClassQueryMasterClock** ](https://msdn.microsoft.com/library/windows/hardware/ff568249)或[ **StreamClassQueryMasterClockSync**](https://msdn.microsoft.com/library/windows/hardware/ff568251).

直到微型驱动程序收到 SRB\_指示\_MASTER\_时钟对于特定的流，它会假定该流没有运行。 如果传入此 SRB 从属固定为相同句柄的句柄传递给微型的驱动程序中[ **SRB\_打开\_MASTER\_时钟**](srb-open-master-clock.md)，微型驱动程序可以直接从主时钟读取时间，因为它可以控制在主机和从属。

微型驱动程序应保留**CommandData.MasterClockHandle**字段指向主时钟的句柄 SRB 中。 如果此句柄为零，它指示微型驱动程序，此流是现在免费运行且不能为属于主时钟。

 

 





