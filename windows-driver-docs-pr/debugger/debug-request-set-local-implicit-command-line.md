---
title: 调试 \_ 请求 \_ 集 \_ 本地 \_ 隐式 \_ 命令 \_ 行
description: 调试 \_ 请求 \_ 集 \_ 本地 \_ 隐式 \_ 命令 \_ 行
keywords:
- DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70f9f9ebc9a1b5fe6678069187cb67805b768267
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803281"
---
# <a name="debug_request_set_local_implicit_command_line"></a>调试 \_ 请求 \_ 集 \_ 本地 \_ 隐式 \_ 命令 \_ 行


"调试 \_ 请求 \_ 集 \_ 本地 \_ 隐式 \_ 命令 \_ 行 [**请求**](request.md) " 操作设置 [调试器引擎](./introduction.md#debugger-engine)的隐式命令行。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新的隐式命令行。 *InBuffer* 的类型为指向 Unicode 字符串 (PWSTR) 的指针。 将复制指针，但不会复制它指向的字符串。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
未使用。

<a name="remarks"></a>备注
-------

创建进程时，可以使用隐式命令行作为命令行。 进程创建选项 ([**调试 \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)) 包含一个选项，用于在创建进程时使用隐式命令行而不是提供的命令行。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**Request**](request.md)

[**调试 \_ 创建 \_ 进程 \_ 选项**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项**](debug-request-get-additional-create-options.md)

[**调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项**](debug-request-set-additional-create-options.md)

[**CreateProcess2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)

[**CreateProcessAndAttach2**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)

 

