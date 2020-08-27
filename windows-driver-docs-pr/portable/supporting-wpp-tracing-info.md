---
description: 支持 WPP 跟踪
title: 支持 WPP 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9110a4ce5f6a689508008806114da257b16337c
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969352"
---
# <a name="supporting-wpp-tracing"></a>支持 WPP 跟踪


Windows 软件跟踪预处理器 (WPP) 提供高效的实时事件日志记录机制。 需要使用 WPP 在 WPD 驱动程序中记录跟踪和错误消息。

WPP 跟踪包括系统时间戳，可用于度量性能，例如，测量函数调用之间经过的时间。

## <a name="span-idsample_drivers_that_support_wpp_tracingspanspan-idsample_drivers_that_support_wpp_tracingspanspan-idsample_drivers_that_support_wpp_tracingspansample-drivers-that-support-wpp-tracing"></a><span id="Sample_Drivers_that_Support_WPP_Tracing"></span><span id="sample_drivers_that_support_wpp_tracing"></span><span id="SAMPLE_DRIVERS_THAT_SUPPORT_WPP_TRACING"></span>支持 WPP 跟踪的示例驱动程序


下面的示例驱动程序演示如何使用 WPP 跟踪：

-   WpdBasicHardwareDriver
-   WpdServiceSampleDriver

## <a name="span-idtransitioning_from_outputdebugstring_to_wppspanspan-idtransitioning_from_outputdebugstring_to_wppspanspan-idtransitioning_from_outputdebugstring_to_wppspantransitioning-from-outputdebugstring-to-wpp"></a><span id="Transitioning_from_OutputDebugString_to_WPP"></span><span id="transitioning_from_outputdebugstring_to_wpp"></span><span id="TRANSITIONING_FROM_OUTPUTDEBUGSTRING_TO_WPP"></span>从 OutputDebugString 转换为 WPP


WpdHelloWorldDriver、WpdWudfSampleDriver 和 WpdMultiTransportDriver 日志错误消息，通过使用 \_ 环绕 **OutputDebugString** 方法的 CHECK HR 函数进行。 尽管在开发期间此方法很容易使用，但它需要一个活动的调试器连接才能查看跟踪。 OutputDebugString 方法应在最终代码中最少使用一次发布。 对于一系列的跟踪应用程序而言，WPP 跟踪更为轻便、灵活和可取：记录用于诊断故障的错误，在开发过程中跟踪代码执行，例如。

若要将驱动程序从使用 **OutputDebugString** 转换为使用 WPP，请完成以下步骤：

1.  删除原始检查 \_ HR ( # A1 函数定义 (可在 *WpdHelloWorldDriver* 或 *WpdWudfSampleDriver* 中找到 WPD 示例) 及其在 *stdafx.h*中的声明。
2.  用 WPP 宏更新 *stdafx.h* 文件，本主题稍后将对此进行介绍。
3.  向 \_ 驱动程序的源文件中添加一个 "运行 WPP" 指令。
4.  向驱动程序的 DllMain 方法添加 WPP 初始化和清理例程。
5.  对于每个驱动程序源文件，请在现有的 include 语句后添加一个* \# include &lt; &gt; tmh*。
6.  重建驱动程序。 由于已将 CHECK \_ hr 函数替换为具有相同签名的等效 WPP 宏，因此使用 CHECK HR 的任何代码都不需要进行任何更改 \_ 。

WPP 预处理器处理跟踪宏的 *stdafx.h* ，并为每个宏生成跟踪消息标头 (tmh) 文件。Obj 文件夹中的 CPP 文件。

如果检查每个的预处理器输出。\_使用 *WpdBaseDriver*) 生成的用于调用检查 HR (的 CPP 文件，你会注意到，所有检查 \_ hr TRACE 语句已被 WPP 函数调用包装，而跟踪文本和 WPP 函数在 *WpdBaseDriver*中定义。

你可能会遇到的与 WPP 相关的最常见编译错误是由于格式标识符和参数不匹配 (例如，如果格式字符串包含一个额外的% d，该% d 与参数) 或在 WPP \_ 控件 guid 宏中缺少项，则为 \_ 。

## <a name="span-idupdating_the_stdafxh_filespanspan-idupdating_the_stdafxh_filespanupdating-the-stdafxh-file"></a><span id="updating_the_stdafx.h_file"></span><span id="UPDATING_THE_STDAFX.H_FILE"></span>更新 Stdafx.h 文件


下面的代码示例包含对 *stdafx.h* 的更新，如果驱动程序当前支持 **OutputDebugString**。

```ManagedCPlusPlus
#define MYDRIVER_TRACING_ID      L"Microsoft\\WPD\\ServiceSampleDriver"

#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(ServiceSampleDriverCtlGuid,(f0cc34b3,a482,4dc0,b978,b5cf42aec4fd), \
        WPP_DEFINE_BIT(TRACE_FLAG_ALL)                                      \
        WPP_DEFINE_BIT(TRACE_FLAG_DEVICE)                                   \
        WPP_DEFINE_BIT(TRACE_FLAG_DRIVER)                                   \
        WPP_DEFINE_BIT(TRACE_FLAG_QUEUE)                                    \
        )

#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)

//
// This comment block is scanned by the trace preprocessor to define our
// TraceEvents function.
//
// begin_wpp config
// FUNC Trace{FLAG=TRACE_FLAG_ALL}(LEVEL, MSG, ...);
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// end_wpp

//
// This comment block is scanned by the trace preprocessor to define our
// CHECK_HR function.
//
//
// begin_wpp config
// USEPREFIX (CHECK_HR,"%!STDPREFIX!");
// FUNC CHECK_HR{FLAG=TRACE_FLAG_ALL}(hrCheck, MSG, ...);
// USESUFFIX (CHECK_HR, " hr= %!HRESULT!", hrCheck);
// end_wpp

//
// PRE macro: The name of the macro includes the condition arguments FLAGS and EXP
//            define in FUNC above
//
#define WPP_FLAG_hrCheck_PRE(FLAGS, hrCheck) {if(hrCheck != S_OK) {

//
// POST macro
// The name of the macro includes the condition arguments FLAGS and EXP
//            define in FUNC above
#define WPP_FLAG_hrCheck_POST(FLAGS, hrCheck) ; } }

//
// The two macros below are for checking if the event should be logged and for
// choosing the logger handle to use when calling the ETW trace API
//
#define WPP_FLAG_hrCheck_ENABLED(FLAGS, hrCheck) WPP_FLAG_ENABLED(FLAGS)
#define WPP_FLAG_hrCheck_LOGGER(FLAGS, hrCheck) WPP_FLAG_LOGGER(FLAGS)
```

## <a name="span-idadding_the_wpp_initialization_and_cleanup_routines_to_dllmainspanspan-idadding_the_wpp_initialization_and_cleanup_routines_to_dllmainspanspan-idadding_the_wpp_initialization_and_cleanup_routines_to_dllmainspanadding-the-wpp-initialization-and-cleanup-routines-to-dllmain"></a><span id="Adding_the_WPP_Initialization_and_Cleanup_Routines_to_DllMain"></span><span id="adding_the_wpp_initialization_and_cleanup_routines_to_dllmain"></span><span id="ADDING_THE_WPP_INITIALIZATION_AND_CLEANUP_ROUTINES_TO_DLLMAIN"></span>向 DllMain 添加 WPP 初始化和清理例程


更新 *源文件* 后，更新驱动程序的 DllMain 例程，如下面的代码示例所示：

```ManagedCPlusPlus
// DLL Entry Point
extern "C" BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID lpReserved)
{    
if(DLL_PROCESS_ATTACH == dwReason)    
{        
g_hInstance = hInstance;              
//        
// Initialize tracing.        
//        
WPP_INIT_TRACING(MYDRIVER_TRACING_ID);    
}    
else if (DLL_PROCESS_DETACH == dwReason)    
{        
//        
// Cleanup tracing.        
//        
WPP_CLEANUP();    
}    
return _AtlModule.DllMain(dwReason, lpReserved);
}
```

## <a name="span-idincluding_the_trace_message_header_filesspanspan-idincluding_the_trace_message_header_filesspanspan-idincluding_the_trace_message_header_filesspanincluding-the-trace-message-header-files"></a><span id="Including_the_Trace_Message_Header_files"></span><span id="including_the_trace_message_header_files"></span><span id="INCLUDING_THE_TRACE_MESSAGE_HEADER_FILES"></span>包括跟踪消息头文件


更新 DllMain 例程后，请更新每个例程。CPP 源文件，并包含相应的跟踪消息标头文件。 下面的代码示例演示如何将 *WpdBaseDriver* 文件包含在 *WpdBaseDriver*中。

```ManagedCPlusPlus
//
// WpdBaseDriver.cpp
//#include "stdafx.h"
#include "WpdBaseDriver.h"
// Include the WPP generated Trace Message Header (tmh) file for this .cpp
#include "WpdBaseDriver.tmh"
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WDK 和 Visual Studio 生成环境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)

 

 





