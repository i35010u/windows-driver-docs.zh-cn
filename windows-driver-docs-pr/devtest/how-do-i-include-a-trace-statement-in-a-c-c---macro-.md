---
title: 如何将跟踪语句包括一个 C 中 /C++宏
description: 如何将跟踪语句包括一个 C 中 /C++宏
ms.assetid: 1ab7f87e-7dbc-49a1-b3a2-24e4d525dc8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ed0afac0f86b5de4aee95003c3008175522e2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329867"
---
# <a name="how-do-i-include-a-trace-statement-in-a-cc-macro"></a>如何在 C/C++ 宏中包含跟踪语句？


严格地说，不能具有宏中的跟踪语句，因为 WPP 预处理器在运行之前 C 预处理器。 一种解决方案是运行 C 预处理器两次，但更简单的解决方案： 定义对跟踪宏的 PRE 和 POST 的可选步骤。

例如，可能会想"退出失败"的宏如

```
If (FAILED(HR)) {
     DoTraceMessage(ERROR,"We failed!");
     Goto done ;
} 
```

在这种情况下，使用宏的 PRE 和 POST 窗体实现此目的。

### <a name="span-iddefinethefunctionspanspan-iddefinethefunctionspandefine-the-function"></a><span id="define_the_function"></span><span id="DEFINE_THE_FUNCTION"></span>定义函数

在源代码文件中，定义函数，例如：

```
FUNC:_EXIT_IF_EXP_FAILED{LEVEL=WSM_ERROR}(_EXIT_IF_EXP_FAILED_EXP,MSG,...)
```

### <a name="span-iddefinethemacrosspanspan-iddefinethemacrosspandefine-the-macros"></a><span id="define_the_macros"></span><span id="DEFINE_THE_MACROS"></span>定义宏

在标头文件中，添加以下定义指令。 将其放后 WPP\_控制\_GUID 定义之前**\#包括**语句[跟踪消息标头文件](trace-message-header-file.md)。

```
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_PRE(LEVEL, HR) {HRESULT hr=S_OK ; if(FAILED(hr = HR)) {
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_POST(LEVEL, HR) ; goto done; } }
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_ENABLED(LEVEL, HR) WPP_LEVEL_ENABLED(LEVEL)
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(WSM_ERROR)
```

### <a name="span-idaddformattingspanspan-idaddformattingspanadd-formatting"></a><span id="add_formatting"></span><span id="ADD_FORMATTING"></span>添加格式设置

您可以使跟踪消息易于阅读的包括格式设置标头文件中的数据。 此步骤可选。

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

在此示例中，**开始\_wpp config**并**最终\_wpp**语句标识为 WPP 标头文件中的配置数据。

此外，若要通知 WPP 标头文件中没有配置数据，添加 **-扫描**参数运行\_WPP 宏调用 WPP 预处理器。 例如：

```
RUN_WPP -scan:trace.h
```

有关运行的可选参数的完整列表\_WPP，请参阅[WPP 预处理器](wpp-preprocessor.md)。

### <a name="span-idusethemacrosspanspan-idusethemacrosspanuse-the-macros"></a><span id="use_the_macros"></span><span id="USE_THE_MACROS"></span>使用宏

在源代码中，在以下调用中使用如宏：

```
_EXIT_IF_EXP_FAILED(hr,"it failed");
```

 

 





