---
title: 调试\_请求\_设置\_本地\_隐式\_命令\_行
description: 调试\_请求\_设置\_本地\_隐式\_命令\_行
ms.assetid: c54fc9f3-2805-4411-8162-18d4f9983795
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
ms.openlocfilehash: 430960b284f37f3d9a63623485adf1d212a8cbd4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361431"
---
# <a name="debugrequestsetlocalimplicitcommandline"></a>调试\_请求\_设置\_本地\_隐式\_命令\_行


调试\_请求\_设置\_本地\_隐式\_命令\_行[**请求**](request.md)操作设置[调试器引擎](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)的隐式命令行。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新的隐式命令行。 类型*InBuffer*指向 Unicode 字符串 (PWSTR) 的指针。 指针将被复制但不能复制它指向的字符串。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
不使用。

<a name="remarks"></a>备注
-------

创建一个过程时，隐式的命令行可用作命令行。 进程创建选项 ([**调试\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)) 包含使用而不是提供的隐式的命令行选项命令行创建一个进程时。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**请求**](request.md)

[**调试\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_create_process_options)

[**DEBUG\_REQUEST\_GET\_ADDITIONAL\_CREATE\_OPTIONS**](debug-request-get-additional-create-options.md)

[**DEBUG\_REQUEST\_SET\_ADDITIONAL\_CREATE\_OPTIONS**](debug-request-set-additional-create-options.md)

[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocess2)

[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)

 

 






