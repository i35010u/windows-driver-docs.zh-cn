---
title: 调试 \_ 请求 \_ 目标 \_ 可以 \_ 分离
description: 调试 \_ 请求 \_ 目标 \_ 可以 \_ 分离
keywords:
- DEBUG_REQUEST_TARGET_CAN_DETACH Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_TARGET_CAN_DETACH
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ca613c607ee6c1ef1ef63462fc75842fa174d41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826933"
---
# <a name="debug_request_target_can_detach"></a>调试 \_ 请求 \_ 目标 \_ 可以 \_ 分离


调试 \_ 请求 \_ 目标 \_ 可以 \_ 分离 [**请求**](request.md) 操作检查，以查看调试器引擎是否可以与当前进程分离 (使进程保持运行，但不再) 调试。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
未使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
未使用。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S \_ 正常  
可以从当前进程分离调试器。

<span id="S_FALSE"></span><span id="s_false"></span>S \_ FALSE  
不能将调试器与当前进程分离。

<a name="remarks"></a>备注
-------

只有在 Microsoft Windows XP 或更高版本的 Windows 上运行的目标才支持从进程中分离调试器。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

 

 






