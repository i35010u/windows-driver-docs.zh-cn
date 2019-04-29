---
title: 调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量
description: 调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量
ms.assetid: cdf05d4f-8a8c-4b52-b36f-9d00575fdb7b
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
ms.openlocfilehash: a6567bbb3032dbcea06789b507221ad555f2b418
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369787"
---
# <a name="debugrequestgetcapturedeventcodeoffset"></a>调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量


调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量[**请求**](request.md)操作返回当前事件的指令指针。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
当前事件的指令指针。 指令指针的类型为 ULONG64。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S\_确定  
此方法已成功。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
在当前事件的指令指针的内存不是有效的。

此方法还可能返回错误值。 请参阅[**返回值**](https://msdn.microsoft.com/library/windows/hardware/ff549771)的更多详细信息。

<a name="remarks"></a>备注
-------

可以使用读取当前事件的指令指针的内存[**请求**](request.md)操作的[**调试\_请求\_读取\_CAPTURED\_事件\_代码\_流**](debug-request-read-captured-event-code-stream.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

[**调试\_请求\_读取\_CAPTURED\_事件\_代码\_流**](debug-request-read-captured-event-code-stream.md)

 

 






