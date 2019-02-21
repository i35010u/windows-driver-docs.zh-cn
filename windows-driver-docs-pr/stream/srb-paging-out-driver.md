---
title: SRB\_PAGING\_OUT\_DRIVER
description: SRB\_PAGING\_OUT\_DRIVER
ms.assetid: 9bcb9f07-6fea-427b-9ae8-afdc6aec540f
keywords:
- SRB_PAGING_OUT_DRIVER 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_PAGING_OUT_DRIVER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1282416ab7aeab03e4e8bf2fe1ab44a906cc8110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524207"
---
# <a name="srbpagingoutdriver"></a>SRB\_PAGING\_OUT\_DRIVER


## <span id="ddk_srb_paging_out_driver_ks"></span><span id="DDK_SRB_PAGING_OUT_DRIVER_KS"></span>


在类驱动程序将发出信号，它是有关此请求发送到页面输出微型驱动程序。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

### <a name="comments"></a>备注

在类驱动程序才会尝试进行分页出微型驱动程序，如果它没有打开的流或设备。 尽管可能性很小，微型驱动程序具有挂起的回调在此状态，微型驱动程序应取消在收到此 SRB 时任何未完成的回调。 微型驱动程序应禁用适配器中断，并返回状态\_成功。

类驱动程序的页面出微型驱动程序仅当微型驱动程序将启用此功能。 微型驱动程序启用此功能通过在设备的 INF 文件中将注册表变量 PageOutWhenUnopened 设置为 1。 查看流式处理的详细信息的微型驱动程序的 Inf 的示例。

 

 





