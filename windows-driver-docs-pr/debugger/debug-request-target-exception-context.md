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
ms.openlocfilehash: 1a48ec1f66ebb7997ac545bbe88d3688fadfaf7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366970"
---
# <a name="debugrequesttargetexceptioncontext"></a>调试\_请求\_目标\_异常\_上下文


调试\_请求\_目标\_异常\_上下文[**请求**](request.md)操作返回[线程上下文](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)中的用户模式的小型转储文件的存储事件。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
存储事件的线程上下文。 线程上下文的类型为目标的有效处理器的上下文结构在事件的时间。 *OutBuffer*必须足够大以保存此结构。

<a name="remarks"></a>备注
-------

此信息也会返回给*上下文*由参数[ **GetStoredEventInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)方法。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

[**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)

 

 






