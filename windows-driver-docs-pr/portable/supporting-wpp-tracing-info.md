---
Description: 支持 WPP 跟踪
title: 支持 WPP 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e94395218c546c06d283b6a66d964bbf8c79fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387184"
---
# <a name="supporting-wpp-tracing"></a>支持 WPP 跟踪


Windows 软件跟踪预处理器 (WPP)，提供了高效的实时事件日志记录机制。 WPP 是 WPD 驱动程序中记录跟踪和错误消息的建议的方法。

WPP 跟踪包含系统时间戳，可以用于衡量性能，例如，通过测量函数调用之间经过的时间。

## <a name="span-idsampledriversthatsupportwpptracingspanspan-idsampledriversthatsupportwpptracingspanspan-idsampledriversthatsupportwpptracingspansample-drivers-that-support-wpp-tracing"></a><span id="Sample_Drivers_that_Support_WPP_Tracing"></span><span id="sample_drivers_that_support_wpp_tracing"></span><span id="SAMPLE_DRIVERS_THAT_SUPPORT_WPP_TRACING"></span>支持 WPP 跟踪的示例驱动程序


下面的示例驱动程序演示如何使用 WPP 跟踪：

-   WpdBasicHardwareDriver
-   WpdServiceSampleDriver

## <a name="span-idtransitioningfromoutputdebugstringtowppspanspan-idtransitioningfromoutputdebugstringtowppspanspan-idtransitioningfromoutputdebugstringtowppspantransitioning-from-outputdebugstring-to-wpp"></a><span id="Transitioning_from_OutputDebugString_to_WPP"></span><span id="transitioning_from_outputdebugstring_to_wpp"></span><span id="TRANSITIONING_FROM_OUTPUTDEBUGSTRING_TO_WPP"></span>从 OutputDebugString 过渡到 WPP


WpdHelloWorldDriver、 WpdWudfSampleDriver 和 WpdMultiTransportDriver 记录错误消息使用检查\_HR 函数来包装**OutputDebugString**方法。 虽然在开发过程中，此方法是易于使用，它将需要的活动的调试器连接，以便查看跟踪。 OutputDebugString 方法应按最小方式在最终代码版本。 WPP 跟踪是更轻量、 灵活且更适用于一系列跟踪应用程序： 为诊断故障，例如跟踪代码执行在开发期间，日志记录错误。

若要转换的驱动程序由使用**OutputDebugString**若要使用 WPP，完成以下步骤：

1.  删除原始复选\_HR() 函数定义 (可在*WpdHelloWorldDriver.cpp*或*WpdWudfSampleDriver.cpp* WPD 示例) 和其声明中*Stdafx.h*。
2.  更新*Stdafx.h*使用 WPP 宏，稍后在本主题中描述了这些文件。
3.  将运行添加\_WPP 指令到您的驱动程序的源代码文件。
4.  添加到您的驱动程序的 DllMain 方法 WPP 初始化和清理例程。
5.  对于每个驱动程序源文件，请添加 *\#包括&lt;filename&gt;.tmh*现有包含语句之后。
6.  重新生成您的驱动程序。 因为替换为复选\_HR 函数与具有相同的签名等效 WPP 宏，无需更改任何使用的代码检查\_HR。

WPP 预处理器进程*Stdafx.h*对于跟踪宏，并为每个生成的跟踪消息标头 (tmh) 文件。Obj 文件夹中的 CPP 文件。

如果为每个检查预处理器输出。CPP 文件调用复选\_HR (生成的使用，请*WpdBaseDriver.pp*)，你注意到所有检查\_WPP 函数调用，同时跟踪文本和 WPP 函数包装 HR 跟踪语句在中定义*WpdBaseDriver.tmh*。

可能会遇到的最常见 WPP 相关的编译错误是由于不匹配的格式标识符和参数 （例如，如果格式字符串包含一个额外 %d 与参数不匹配） 或缺失的条目中 WPP\_控件\_GUID 宏。

## <a name="span-idupdatingthestdafxhfilespanspan-idupdatingthestdafxhfilespanupdating-the-stdafxh-file"></a><span id="updating_the_stdafx.h_file"></span><span id="UPDATING_THE_STDAFX.H_FILE"></span>正在更新 Stdafx.h 文件


下面的代码示例包含要对进行的更新*Stdafx.h*如果您的驱动程序目前支持**OutputDebugString**。

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

## <a name="span-idaddingthewppinitializationandcleanuproutinestodllmainspanspan-idaddingthewppinitializationandcleanuproutinestodllmainspanspan-idaddingthewppinitializationandcleanuproutinestodllmainspanadding-the-wpp-initialization-and-cleanup-routines-to-dllmain"></a><span id="Adding_the_WPP_Initialization_and_Cleanup_Routines_to_DllMain"></span><span id="adding_the_wpp_initialization_and_cleanup_routines_to_dllmain"></span><span id="ADDING_THE_WPP_INITIALIZATION_AND_CLEANUP_ROUTINES_TO_DLLMAIN"></span>添加对 DllMain 的 WPP 初始化和清理例程


更新后*源*文件中，更新该驱动程序，DllMain 例程，如下面的代码示例中所示：

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

## <a name="span-idincludingthetracemessageheaderfilesspanspan-idincludingthetracemessageheaderfilesspanspan-idincludingthetracemessageheaderfilesspanincluding-the-trace-message-header-files"></a><span id="Including_the_Trace_Message_Header_files"></span><span id="including_the_trace_message_header_files"></span><span id="INCLUDING_THE_TRACE_MESSAGE_HEADER_FILES"></span>包括跟踪消息标头文件


更新 DllMain 例程后，更新每个。CPP 源文件，并包括相应的跟踪消息标头文件。 下面的代码示例显示了包含*WpdBaseDriver.tmh*中的文件*WpdBaseDriver.cpp*。

```ManagedCPlusPlus
//
// WpdBaseDriver.cpp
//#include "stdafx.h"
#include "WpdBaseDriver.h"
// Include the WPP generated Trace Message Header (tmh) file for this .cpp
#include "WpdBaseDriver.tmh"
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WDK 和 Visual Studio 生成环境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)

 

 





