---
title: 调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项
description: 调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项
keywords:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06b2ebc281c383490513884ec9427c116201fcd3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791631"
---
# <a name="debug_request_set_additional_create_options"></a>调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项


"调试 \_ 请求 \_ 设置 \_ 其他 \_ 创建 \_ 选项" [**请求**](request.md) 操作设置默认进程创建选项。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新的默认进程创建选项。 进程创建选项的类型为 "调试" " [**\_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)"。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
未使用。

<a name="remarks"></a>备注
-------

默认进程创建选项用于方法 [**CreateProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess) 和 [**CreateProcessAndAttach**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach) ，与 [**CreateProcess2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2) 和 [**CreateProcessAndAttach2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)不同，它们不指定进程创建选项的全部范围。

由于所有进程创建操作都提供此信息，因此 "[**调试 \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)" 结构的 " **CreateFlags** " 字段不会用作默认值。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

[**调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项**](debug-request-get-additional-create-options.md)

[**调试 \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**CreateProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess)

[**CreateProcessAndAttach**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach)

 

