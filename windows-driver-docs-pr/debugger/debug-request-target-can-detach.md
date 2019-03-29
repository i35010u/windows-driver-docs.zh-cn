---
title: 调试\_请求\_目标\_可以\_分离
description: 调试\_请求\_目标\_可以\_分离
ms.assetid: 1e36715e-3414-4cd2-95f3-2b97878a3989
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
ms.openlocfilehash: c5bfc79d7b0e607a14a6500adfc84608e9ae0990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575993"
---
# <a name="debugrequesttargetcandetach"></a>调试\_请求\_目标\_可以\_分离


调试\_请求\_目标\_可以\_分离[**请求**](request.md)操作检查是否可以为调试器引擎从分离当前进程 （离开进程正在运行但不能再调试）。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
不使用。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S\_确定  
就可以将调试器与当前进程分离。

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
不能将调试器与当前进程分离。

<a name="remarks"></a>备注
-------

仅 Microsoft Windows XP 或更高版本的 Windows 上运行的目标都支持调试器与进程分离。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

 

 






