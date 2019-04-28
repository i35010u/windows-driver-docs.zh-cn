---
title: 调用 TraceMessage 之前可以保留的最后一个错误代码
description: 调用 TraceMessage 之前可以保留的最后一个错误代码
ms.assetid: 57390fb1-5e01-4b98-960f-0201213d673c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea0614ceee3bc10330bebb08786c36b041c47666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344917"
---
# <a name="can-i-preserve-the-last-error-code-before-tracemessage-is-called"></a>是否可以在调用 TraceMessage 之前保留最后一个错误代码？


默认情况下[TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)使用 WPP 调用\_TRACE 宏。 在早于 Windows Vista 的 Windows 版本[最后一个错误代码](https://go.microsoft.com/fwlink/p/?linkid=179346)已覆盖**TraceMessage**。

从 Windows Vista 开始，你可以通过定义自定义 WPP 保留上一个错误代码\_TRACE 宏。 包括在内之前，必须定义此宏的版本[跟踪消息标头 (.tmh) 文件](trace-message-header-file.md)的源文件中您[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序...

下面的示例演示如何在调用之前保留的最后一个错误代码**TraceMessage**:

-   请到包装**TraceMessage**调用从 WPP\_TRACE 宏。 然后，可以调用[TraceMessageVa](https://go.microsoft.com/fwlink/p/?linkid=179352)，从包装器函数。

    下面的示例演示如何编写的包装**TraceMessage**:

    ```
    #define WPP_TRACE WppTraceMessageWrapper
    DWORD
    WppTraceMessageWrapper(
        __in TRACEHANDLE LoggerHandle,
        __in ULONG MessageFlags,
        __in LPCGUID MessageGuid,
        __in USHORT Message Number,
        ...)
    {
        DWORD TraceError = ERROR_SUCCESS;
        DWORD LastError = ERROR_SUCCESS;
        va_list Args = NULL;
     
        LastError = GetLastError();
     
        va_start(Args, Message Number);
        TraceError = TraceMessageVa(LoggerHandle, MessageFlags, MessageGuid, Message Number, Args);
        va_end(Args);
     
        SetLastError(LastError);
     return TraceError;
    }
    ```

-   修改 WPP\_TRACE 宏，如下面的示例中所示：
    ```
    #define WPP_TRACE(...)                              \
     do                                              \
        {                                               \
            DWORD LastError = GetLastError();           \
            TraceMessage(__VA_ARGS__);                  \
            SetLastError(LastError);                    \
        }                                               \
     while (FALSE, FALSE)
    ```

    **请注意**  此方法会增加您的二进制文件的代码大小，因为相同的代码将生成每个 WPP\_SF 函数。

     

 

 





