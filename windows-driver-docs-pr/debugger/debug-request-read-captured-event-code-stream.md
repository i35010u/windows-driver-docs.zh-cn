---
title: 调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流
description: 调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流
keywords:
- DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 541550ac2746fdecc0cfb01c7019818e2f647de3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791991"
---
# <a name="debug_request_read_captured_event_code_stream"></a>调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流


"调试 \_ 请求 \_ 读取 \_ 捕获 \_ \_ 的事件代码 \_ 流 [**请求**](request.md) " 操作在当前事件的指令指针上最多返回64字节的内存。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
未使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
当前事件的指令指针处的内存。 最多可以返回64字节的内存。

<a name="remarks"></a>备注
-------

返回的内存是事件发生时所占用内存的快照。 它不反映自事件以来可能已对目标的内存进行的任何更改。

当前事件的指令指针由 [**请求**](request.md) 操作 [**DEBUG \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量**](debug-request-get-captured-event-code-offset.md)返回。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

[**调试 \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量**](debug-request-get-captured-event-code-offset.md)

 

 






