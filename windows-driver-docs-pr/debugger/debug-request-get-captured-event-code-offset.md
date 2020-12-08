---
title: 调试 \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量
description: 调试 \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量
keywords:
- DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6af1d255b7c29209d480b1485374c1867c787eeb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787787"
---
# <a name="debug_request_get_captured_event_code_offset"></a>调试 \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量


"调试 \_ 请求 \_ 获取 \_ 捕获 \_ \_ 的事件代码 \_ 偏移量 [**请求**](request.md) " 操作返回当前事件的指令指针。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
未使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
当前事件的指令指针。 指令指针的类型为 ULONG64。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S \_ 正常  
方法成功。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E \_ NOINTERFACE  
当前事件的指令指针处的内存无效。

此方法可能还会返回错误值。 有关更多详细信息，请参阅 [**返回值**](./hresult-values.md) 。

<a name="remarks"></a>备注
-------

可以使用 [**请求**](request.md) 操作的 [**调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流**](debug-request-read-captured-event-code-stream.md)来读取当前事件的指令指针处的内存。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

[**调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流**](debug-request-read-captured-event-code-stream.md)

 

