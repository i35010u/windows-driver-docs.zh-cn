---
title: 如何修复 TraceLogging 生成错误
description: 本主题介绍一些常见的生成错误和如何解决这些问题。
ms.assetid: E0C7ACA5-68C9-40FF-8D6E-4A65CEB0A851
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3dab8293ffad7098dc400309a84c0d163786052
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329939"
---
# <a name="how-to-fix-tracelogging-build-errors"></a>如何修复 TraceLogging 生成错误


本主题介绍一些常见的生成错误和如何解决这些问题。

## <a name="span-idcase1declspecsafebufferserrorsspanspan-idcase1declspecsafebufferserrorsspanspan-idcase1declspecsafebufferserrorsspancase-1-declspecsafebuffers-errors"></a><span id="Case_1___DECLSPEC_SAFEBUFFERS__errors"></span><span id="case_1___declspec_safebuffers__errors"></span><span id="CASE_1___DECLSPEC_SAFEBUFFERS__ERRORS"></span>案例 1：DECLSPEC\_SAFEBUFFERS' 错误


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>生成错误 （代码段）：  
```
1>traceloggingprovider.h(1592): error C2146: syntax error : missing ';' before identifier 'TLG_STATUS'
1>traceloggingprovider.h(1592): error C2433: 'DECLSPEC_SAFEBUFFERS' : 'inline' not permitted on data declarations
1>traceloggingprovider.h(1592): error C4430: missing type specifier - int assumed. Note: C++ does not support default-int
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>解决方法：  
在源文件中包含 TraceLoggingProvider.h 之前包括 windows.h。

## <a name="span-idcase2tracelogginginmoderncappsspanspan-idcase2tracelogginginmoderncappsspanspan-idcase2tracelogginginmoderncappsspancase-2-tracelogging-in-modern-c-apps"></a><span id="Case_2__TraceLogging_in_Modern_C___Apps"></span><span id="case_2__tracelogging_in_modern_c___apps"></span><span id="CASE_2__TRACELOGGING_IN_MODERN_C___APPS"></span>案例 2：现代版中的 TraceLoggingC++应用程序


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>生成错误 （代码段）：  
之后将 TraceLogging 标头文件复制到你的生成环境并添加以下行：

```
TraceLoggingRegisterByGuid(g_3DBuilderTraceProvider, &s_3DBuilderTraceProviderGuid);
```

获取此链接器错误：

```
Error 2 error LNK2001: unresolved external symbol __imp__EventSetInformation@20 
        E:\TFS\Main\PrintPreviewR5\Viewers\PrintPreview\App.xaml.obj    PrintPreview
Error 3 error LNK2001: unresolved external symbol __imp__EventRegister@16       
        E:\TFS\Main\PrintPreviewR5\Viewers\PrintPreview\App.xaml.obj    PrintPreview
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>解决方法：  
UWP 应用需要针对 advapi32.lib 若要解决此引用问题进行链接。

## <a name="span-idcase3phonebuildsspanspan-idcase3phonebuildsspanspan-idcase3phonebuildsspancase-3-phone-builds"></a><span id="Case_3__Phone_Builds"></span><span id="case_3__phone_builds"></span><span id="CASE_3__PHONE_BUILDS"></span>案例 3：电话版本


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>生成错误 （代码段）：  
在编译时文件 dictationuimodel.cpp，你将收到错误：

```
traceloggingprovider.h(1592) : error C2146: syntax error : missing ';' before identifier 'TLG_STATUS'
traceloggingprovider.h(1592) : error C2433: 'DECLSPEC_SAFEBUFFERS' : 'inline' not permitted on data declarations
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>解决方法：  
请参阅用例\#1。 很可能你的 SDK 不定义宏**DECLSPEC\_SAFEBUFFERS**。 最新 Sdk 会为此宏的定义。 如果 SDK 未定义此宏，你将需要提供自己的定义。 **DECLSPEC\_SAFEBUFFERS** winnt.h，应包括通过 windows.h 中定义。 此外，Windows 10 SDK 的公共版本发布之前可能需要定义*遥测*关键字：

```
#ifndef WINEVENT_KEYWORD_TELEMETRY 
#define WINEVENT_KEYWORD_TELEMETRY  0x2000000000000
#endif
```

 

 





