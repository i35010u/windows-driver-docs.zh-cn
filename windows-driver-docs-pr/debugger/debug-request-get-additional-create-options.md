---
title: 调试\_请求\_获取\_其他\_创建\_选项控制代码
description: 调试\_请求\_获取\_其他\_CREATE\_OPTIONS 请求操作返回默认的进程创建选项。
ms.assetid: ad4c98d9-ca4e-4ee3-a177-2fe04a8f22e2
keywords:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS 控件代码 Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8a95b7d04171960dc980a4d83250c52ec6832ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837792"
---
# <a name="debug_request_get_additional_create_options-control-code"></a>调试\_请求\_获取\_其他\_创建\_选项控制代码


调试\_请求\_获取\_其他\_CREATE\_OPTIONS[**请求**](request.md)操作返回默认的进程创建选项。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
不使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
默认进程创建选项。 进程创建选项的类型为[**DEBUG\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)。

<a name="remarks"></a>备注
-------

默认进程创建选项用于方法[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)和[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach) ，与[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)和[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)不同，它们不指定进程创建选项的全部范围。

[**调试\_CREATE\_PROCESS\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)结构的 " **CreateFlags** " 字段不用作默认结构，因为所有进程创建操作都提供此信息。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**需要**](request.md)

[**调试\_请求\_集\_其他\_创建\_选项**](debug-request-set-additional-create-options.md)

[**调试\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

 






