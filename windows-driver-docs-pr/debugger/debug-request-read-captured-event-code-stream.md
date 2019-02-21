---
title: 调试\_请求\_读取\_CAPTURED\_事件\_代码\_流
description: 调试\_请求\_读取\_CAPTURED\_事件\_代码\_流
ms.assetid: 867c6b3e-13d5-46ae-b73c-f90936cb35c5
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
ms.openlocfilehash: f5d08c61fe7014d5b3fc04c200f882e795693a78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548005"
---
# <a name="debugrequestreadcapturedeventcodestream"></a>调试\_请求\_读取\_CAPTURED\_事件\_代码\_流


调试\_请求\_读取\_CAPTURED\_事件\_代码\_流[**请求**](request.md)操作将返回最多64 个字节的内存在当前事件的指令指针。

**参数**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
在当前事件的指令指针的内存。 最多 64 个字节的内存可能会返回。

<a name="remarks"></a>备注
-------

内存的快照会在事件发生时返回的内存。 它不反映可能已推出的目标内存事件的任何更改。

返回当前事件的指令指针[**请求**](request.md)操作[**调试\_请求\_获取\_捕获\_事件\_代码\_偏移量**](debug-request-get-captured-event-code-offset.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

[**调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量**](debug-request-get-captured-event-code-offset.md)

 

 






