---
title: 调试 \_ 请求 \_ 目标 \_ 异常 \_ 上下文
description: 调试 \_ 请求 \_ 目标 \_ 异常 \_ 上下文
keywords:
- DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 835e1b35411f31f9da9652a4512995f2e03f9c73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824665"
---
# <a name="debug_request_target_exception_context"></a>调试 \_ 请求 \_ 目标 \_ 异常 \_ 上下文


"调试 \_ 请求 \_ 目标 \_ 异常 \_ 上下文 [**请求**](request.md) " 操作返回用户模式小型转储文件中存储的事件的 [线程上下文](./scopes-and-symbol-groups.md#thread-context) 。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
未使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
存储事件的线程上下文。 线程上下文的类型是事件发生时目标的有效处理器的上下文结构。 *OutBuffer* 必须足够大才能容纳此结构。

<a name="remarks"></a>备注
-------

此信息也由 [**GetStoredEventInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)方法返回到 *上下文* 参数。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

[**GetStoredEventInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)

 

