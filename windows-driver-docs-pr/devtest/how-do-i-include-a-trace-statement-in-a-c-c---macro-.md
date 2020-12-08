---
title: 如何实现在 C/c + + 宏中包含跟踪语句
description: 如何实现在 C/c + + 宏中包含跟踪语句
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e23c394445c6e43ec5460b4b888a0f59e56f64bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799765"
---
# <a name="how-do-i-include-a-trace-statement-in-a-cc-macro"></a>如何在 C/C++ 宏中包含跟踪语句？


严格地说，宏中不能有 trace 语句，因为 WPP 预处理器在 C 预处理器之前运行。 一种解决方法是运行 C 预处理器两次，但有一个更简单的解决方案：在跟踪宏中定义可选的前置和后步骤。

例如，你可能需要 "失败时退出" 宏，如

```
If (FAILED(HR)) {
     DoTraceMessage(ERROR,"We failed!");
     Goto done ;
} 
```

在这种情况下，使用宏的 PRE 和 POST 形式可以实现此功能。

### <a name="span-iddefine_the_functionspanspan-iddefine_the_functionspandefine-the-function"></a><span id="define_the_function"></span><span id="DEFINE_THE_FUNCTION"></span>定义函数

在源文件中，定义函数，例如：

```
FUNC:_EXIT_IF_EXP_FAILED{LEVEL=WSM_ERROR}(_EXIT_IF_EXP_FAILED_EXP,MSG,...)
```

### <a name="span-iddefine_the_macrosspanspan-iddefine_the_macrosspandefine-the-macros"></a><span id="define_the_macros"></span><span id="DEFINE_THE_MACROS"></span>定义宏

在标头文件中，添加以下定义指令。 将其置于 WPP \_ 控件 \_ guid 定义之后、[跟踪消息头文件](trace-message-header-file.md)的 **\# include** 语句前面。

```
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_PRE(LEVEL, HR) {HRESULT hr=S_OK ; if(FAILED(hr = HR)) {
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_POST(LEVEL, HR) ; goto done; } }
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_ENABLED(LEVEL, HR) WPP_LEVEL_ENABLED(LEVEL)
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(WSM_ERROR)
```

### <a name="span-idadd_formattingspanspan-idadd_formattingspanadd-formatting"></a><span id="add_formatting"></span><span id="ADD_FORMATTING"></span>添加格式

可以通过在标头文件中包含格式设置数据来使跟踪消息更易于读取。 此步骤是可选的。

```
// MACRO: _EXIT_IF_EXP_FAILED
//
// begin_wpp config
// USEPREFIX (_EXIT_IF_EXP_FAILED,"%!STDPREFIX!");
// FUNC _EXIT_IF_EXP_FAILED{LEVEL=WSM_ERROR}(_EXIT_IF_EXP_FAILED_EXP,MSG,...);
// USESUFFIX (_EXIT_IF_EXP_FAILED," hr= %!HRESULT!", hr);
// end_wpp
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_PRE(LEVEL, HR) {HRESULT hr=S_OK ; if(FAILED(hr = HR)) {
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_POST(LEVEL, HR) ; goto done; } }
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_ENABLED(TRACELEVEL, HR) WPP_LEVEL_ENABLED(TRACELEVEL)
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(WSM_ERROR)
```

在此示例中， **begin \_ wpp config** 和 **end \_ wpp** 语句标识用于 wpp 的标头文件中的配置数据。

此外，若要通知 WPP 在标头文件中存在配置数据，请将 **-scan** 参数添加到 \_ 调用 wpp 预处理器的 RUN WPP 宏。 例如：

```
RUN_WPP -scan:trace.h
```

有关运行 WPP 的可选参数的完整列表 \_ ，请参阅 [WPP 预处理器](wpp-preprocessor.md)。

### <a name="span-iduse_the_macrosspanspan-iduse_the_macrosspanuse-the-macros"></a><span id="use_the_macros"></span><span id="USE_THE_MACROS"></span>使用宏

在源代码中，使用宏，如以下调用中的：

```
_EXIT_IF_EXP_FAILED(hr,"it failed");
```

 

 





