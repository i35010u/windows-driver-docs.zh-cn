---
title: 调试\_请求\_目标\_异常\_上下文
description: 调试\_请求\_目标\_异常\_上下文
ms.assetid: e599a3f7-110b-46fc-8266-3a00ea1efe03
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
ms.openlocfilehash: 4d1047beb623879bf8af9abb9c9b26c57c56a334
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837779"
---
# <a name="debug_request_target_exception_context"></a>调试\_请求\_目标\_异常\_上下文


调试\_请求\_目标\_异常\_上下文[**请求**](request.md)操作在用户模式小型转储文件中返回存储事件的[线程上下文](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
存储事件的线程上下文。 线程上下文的类型是事件发生时目标的有效处理器的上下文结构。 *OutBuffer*必须足够大才能容纳此结构。

<a name="remarks"></a>备注
-------

此信息也由[**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)方法返回到*上下文*参数。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**需要**](request.md)

[**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)

 

 






