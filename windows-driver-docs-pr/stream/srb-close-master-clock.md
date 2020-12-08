---
title: SRB \_ 关闭 \_ 主 \_ 时钟
description: SRB \_ 关闭 \_ 主 \_ 时钟
keywords:
- SRB_CLOSE_MASTER_CLOCK 流媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_MASTER_CLOCK
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabb14c5cf1b432c546d017280f847b8366b674b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814853"
---
# <a name="srb_close_master_clock"></a>SRB \_ 关闭 \_ 主 \_ 时钟


## <span id="ddk_srb_close_master_clock_ks"></span><span id="DDK_SRB_CLOSE_MASTER_CLOCK_KS"></span>


类驱动程序发出此请求，向流表明它不再是微型驱动程序的主时钟。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

 

 





