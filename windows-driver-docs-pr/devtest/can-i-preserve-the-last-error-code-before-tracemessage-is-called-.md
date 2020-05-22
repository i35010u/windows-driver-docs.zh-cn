---
title: 在调用 TraceMessage 之前，是否可以保留最后一个错误的代码
description: 在调用 TraceMessage 之前，是否可以保留最后一个错误的代码
ms.assetid: 57390fb1-5e01-4b98-960f-0201213d673c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8305e09a0707cad2bf7a97f2ec40f8141db502de
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769643"
---
# <a name="can-i-preserve-the-last-error-code-before-tracemessage-is-called"></a>是否可以在调用 TraceMessage 之前保留最后一个错误代码？


默认情况下[TraceMessage](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessage) ，使用 WPP 跟踪宏调用 TraceMessage \_ 。 在早于 Windows Vista 的 Windows 版本中， **TraceMessage**覆盖了[最后一个错误代码](https://docs.microsoft.com/windows/win32/debug/last-error-code)。

从 Windows Vista 开始，可以通过定义自定义 WPP 跟踪宏来保留最后一个错误代码 \_ 。 必须先定义此宏的版本，然后才能将[跟踪消息头（. tmh）文件](trace-message-header-file.md)包含在[跟踪提供程序](trace-provider.md)的源文件中，例如内核模式驱动程序或用户模式应用程序。

下面的示例演示如何在调用**TraceMessage**之前保留最后一个错误代码：

-   创建从 WPP 跟踪宏调用的**TraceMessage**的包装器 \_ 。 然后，可以从包装函数调用[TraceMessageVa](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessageva)。

    下面的示例演示如何将包装器写入**TraceMessage**：

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

-   修改 WPP \_ 跟踪宏，如以下示例中所示：
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

    **注意**   此方法增加了二进制文件的代码大小，因为将为每个 WPP SF 函数生成相同的代码 \_ 。

     

 

 





