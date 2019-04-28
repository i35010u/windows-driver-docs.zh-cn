---
title: 调试\_请求\_获取\_其他\_创建\_选项控制代码
description: 调试\_请求\_获取\_其他\_创建\_选项请求的操作将返回默认进程创建选项。
ms.assetid: ad4c98d9-ca4e-4ee3-a177-2fe04a8f22e2
keywords:
- Windows 调试 DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS 控制代码
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5baa68d958e495a31633cf1d15936c6e7d1becd1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349063"
---
# <a name="debugrequestgetadditionalcreateoptions-control-code"></a>调试\_请求\_获取\_其他\_创建\_选项控制代码


调试\_请求\_获取\_其他\_创建\_选项[**请求**](request.md)操作将返回默认进程创建选项。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
默认过程创建选项。 进程创建选项的类型是[**调试\_创建\_进程\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541464)。

<a name="remarks"></a>备注
-------

方法使用的默认进程创建选项[ **CreateProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff539321)并[ **CreateProcessAndAttach** ](https://msdn.microsoft.com/library/windows/hardware/ff540048)这与不同[**CreateProcess2** ](https://msdn.microsoft.com/library/windows/hardware/ff539323)并[ **CreateProcessAndAttach2**](https://msdn.microsoft.com/library/windows/hardware/ff540055)，未指定进程创建选项的完整范围。

**CreateFlags**字段[**调试\_创建\_过程\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541464)结构不使用默认情况下，因为所有进程创建操作提供此信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

[**DEBUG\_REQUEST\_SET\_ADDITIONAL\_CREATE\_OPTIONS**](debug-request-set-additional-create-options.md)

[**调试\_创建\_进程\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff541464)

[**CreateProcess**](https://msdn.microsoft.com/library/windows/hardware/ff539321)

[**CreateProcessAndAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540048)

 

 






