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
ms.openlocfilehash: 3529e081b8f42125626cf2b48165496cf9cdd497
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837786"
---
# <a name="debug_request_set_local_implicit_command_line"></a>调试\_请求\_设置\_本地\_隐式\_命令\_行


调试\_请求\_集\_本地\_隐式\_命令\_行[**请求**](request.md)操作设置[调试器引擎](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)的隐式命令行。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
新的隐式命令行。 *InBuffer*的类型为指向 Unicode 字符串（PWSTR）的指针。 将复制指针，但不会复制它指向的字符串。

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
不使用。

<a name="remarks"></a>备注
-------

创建进程时，可以使用隐式命令行作为命令行。 创建进程时，进程创建选项（[**调试\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)）包含一个选项，用于使用隐式命令行而不是提供的命令行。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**需要**](request.md)

[**调试\_创建\_进程\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_create_process_options)

[**调试\_请求\_获取\_其他\_创建\_选项**](debug-request-get-additional-create-options.md)

[**调试\_请求\_集\_其他\_创建\_选项**](debug-request-set-additional-create-options.md)

[**CreateProcess2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocess2)

[**CreateProcessAndAttach2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createprocessandattach2)

 

 






