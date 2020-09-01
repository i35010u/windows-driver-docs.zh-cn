---
title: 调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项控制代码
description: "\"调试 \\_ 请求 \\_ 获取 \\_ 其他 \\_ 创建 \\_ 选项\" 请求操作返回默认进程创建选项。"
ms.assetid: ad4c98d9-ca4e-4ee3-a177-2fe04a8f22e2
keywords:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS 控制代码 Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c20656086a9737f66a666992c87ab6b6730b0519
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217885"
---
# <a name="debug_request_get_additional_create_options-control-code"></a>调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项控制代码


"调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项" [**请求**](request.md) 操作返回默认进程创建选项。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
未使用。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
默认进程创建选项。 进程创建选项的类型为 "调试" " [** \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)"。

<a name="remarks"></a>备注
-------

默认进程创建选项用于方法 [**CreateProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess) 和 [**CreateProcessAndAttach**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach) ，与 [**CreateProcess2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2) 和 [**CreateProcessAndAttach2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)不同，它们不指定进程创建选项的全部范围。

由于所有进程创建操作都提供此信息，因此 "[**调试 \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)" 结构的 " **CreateFlags** " 字段不会用作默认值。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

[**调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项**](debug-request-set-additional-create-options.md)

[**调试 \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

