---
title: SRB \_ 分页 \_ 输出 \_ 驱动程序
description: SRB \_ 分页 \_ 输出 \_ 驱动程序
keywords:
- SRB_PAGING_OUT_DRIVER 流媒体设备
topic_type:
- apiref
api_name:
- SRB_PAGING_OUT_DRIVER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a4dada8579525822d962ae659234b92ce2c3af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782019"
---
# <a name="srb_paging_out_driver"></a>SRB \_ 分页 \_ 输出 \_ 驱动程序


## <span id="ddk_srb_paging_out_driver_ks"></span><span id="DDK_SRB_PAGING_OUT_DRIVER_KS"></span>


类驱动程序将发送此请求，通知它即将微型驱动程序。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应将以下内容之一设置为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

### <a name="comments"></a>注释

如果类驱动程序没有打开的流或设备，则仅尝试对微型驱动程序进行分页。 尽管微型驱动程序不太可能在此状态下有挂起的回调，但在收到此 SRB 后，微型驱动程序应取消所有未完成的回调。 微型驱动程序应禁用适配器中断，然后返回状态 " \_ 成功"。

仅当微型驱动程序启用此功能时，类驱动程序才会对微型驱动程序进行分页。 微型驱动程序通过将设备 INF 文件中的注册表变量 PageOutWhenUnopened 设置为1来启用此功能。 有关详细信息，请参阅示例流式处理微型驱动程序。

 

 





