---
title: 如何修复 TraceLogging 生成错误
description: 本主题介绍一些常见的生成错误以及如何解决这些错误。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1121a9c87f633409a5d00b8020e89c359c69d7a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803579"
---
# <a name="how-to-fix-tracelogging-build-errors"></a>如何修复 TraceLogging 生成错误


本主题介绍一些常见的生成错误以及如何解决这些错误。

## <a name="span-idcase_1___declspec_safebuffers__errorsspanspan-idcase_1___declspec_safebuffers__errorsspanspan-idcase_1___declspec_safebuffers__errorsspancase-1-declspec_safebuffers-errors"></a><span id="Case_1___DECLSPEC_SAFEBUFFERS__errors"></span><span id="case_1___declspec_safebuffers__errors"></span><span id="CASE_1___DECLSPEC_SAFEBUFFERS__ERRORS"></span>案例1： "DECLSPEC \_ SAFEBUFFERS" 个错误


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>) 段 (生成错误：  
```
1>traceloggingprovider.h(1592): error C2146: syntax error : missing ';' before identifier 'TLG_STATUS'
1>traceloggingprovider.h(1592): error C2433: 'DECLSPEC_SAFEBUFFERS' : 'inline' not permitted on data declarations
1>traceloggingprovider.h(1592): error C4430: missing type specifier - int assumed. Note: C++ does not support default-int
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>能够  
在源文件中包含 TraceLoggingProvider 之前，请先包含 windows .h。

## <a name="span-idcase_2__tracelogging_in_modern_c___appsspanspan-idcase_2__tracelogging_in_modern_c___appsspanspan-idcase_2__tracelogging_in_modern_c___appsspancase-2-tracelogging-in-modern-c-apps"></a><span id="Case_2__TraceLogging_in_Modern_C___Apps"></span><span id="case_2__tracelogging_in_modern_c___apps"></span><span id="CASE_2__TRACELOGGING_IN_MODERN_C___APPS"></span>案例2：新式 c + + 应用中的 TraceLogging


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>) 段 (生成错误：  
将 TraceLogging 头文件复制到生成环境并添加以下行后：

```
TraceLoggingRegisterByGuid(g_3DBuilderTraceProvider, &s_3DBuilderTraceProviderGuid);
```

您收到了此链接器错误：

```
Error 2 error LNK2001: unresolved external symbol __imp__EventSetInformation@20 
        E:\TFS\Main\PrintPreviewR5\Viewers\PrintPreview\App.xaml.obj    PrintPreview
Error 3 error LNK2001: unresolved external symbol __imp__EventRegister@16       
        E:\TFS\Main\PrintPreviewR5\Viewers\PrintPreview\App.xaml.obj    PrintPreview
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>能够  
UWP 应用需要链接到 advapi32.dll 才能解决此引用问题。

## <a name="span-idcase_3__phone_buildsspanspan-idcase_3__phone_buildsspanspan-idcase_3__phone_buildsspancase-3-phone-builds"></a><span id="Case_3__Phone_Builds"></span><span id="case_3__phone_builds"></span><span id="CASE_3__PHONE_BUILDS"></span>案例3：电话生成


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>) 段 (生成错误：  
在编译文件 dictationuimodel 时，会收到以下错误：

```
traceloggingprovider.h(1592) : error C2146: syntax error : missing ';' before identifier 'TLG_STATUS'
traceloggingprovider.h(1592) : error C2433: 'DECLSPEC_SAFEBUFFERS' : 'inline' not permitted on data declarations
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>能够  
请参阅 Case \# 1。 你的 SDK 可能不会定义宏 **DECLSPEC \_ SAFEBUFFERS**。 最新的 Sdk 具有此宏的定义。 如果 SDK 未定义此宏，则需要提供自己的定义。 **DECLSPEC \_SAFEBUFFERS** 是在由 windows .h 提供的 winnt .h 中定义的。 另外，在 Windows 10 SDK 的公共版本发布之前，你可能需要定义 *遥测* 关键字：

```
#ifndef WINEVENT_KEYWORD_TELEMETRY 
#define WINEVENT_KEYWORD_TELEMETRY  0x2000000000000
#endif
```

 

 





