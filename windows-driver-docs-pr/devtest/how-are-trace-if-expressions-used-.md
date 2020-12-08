---
title: 如何使用 Trace-If 表达式
description: 如何使用 Trace-If 表达式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 897fb455ec7a6907062732d0d4e6b47f16202198
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831549"
---
# <a name="how-are-trace-if-expressions-used"></a>如何使用 Trace-If 表达式？


为了帮助您了解如何使用 Trace-If 表达式，我们提供了一个示例，演示了 "begin \_ wpp config" 语句的用法和语法。 此示例引用函数跟踪 \_ 返回，如果表达式失败 (HR) 为 true，则会记录事件。

如果失败 (HR) 为 true，则假定存在具有状态 ULONG 的源文件，并将通过调用 TRACE \_ RETURN (status) 记录事件。
```
//MACRO: TRACE_RETURN
//
//begin_wpp config
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
//end_wpp

#define WPP_LEVEL_EXP_PRE(LEVEL, HR) {if (FAILED(HR)) {
#define WPP_LEVEL_EXP_POST(LEVEL, HR) ;}}
#define WPP_LEVEL_EXP_ENABLED(LEVEL, HR) WPP_LEVEL_ENABLED(LEVEL)
#define WPP_LEVEL_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(ERROR)
```

在上面的示例中，请注意，TRACE \_ RETURN 在 begin \_ wpp config 和 end \_ wpp 行之间定义。 然后，此定义后跟 PRE/POST 宏以及 ENABLED 和记录器定义。

Begin \_ wpp config 和 end \_ wpp 分隔符定义由预处理器分析的配置块。 必须通过 WPP 扫描包含配置块定义的文件。 此文件是用-scan： file. extension 参数指定的。

**注意**   有关 **-扫描** 和其他 **运行 \_ wpp** 选项的信息，请参阅 [WPP 预处理器](wpp-preprocessor.md)。



以下列表提供了有关示例配置块中每个语句的详细信息：

<span id="USEPREFIX"></span><span id="useprefix"></span>**USEPREFIX**  
定义要在记录事件时使用的前缀格式字符串。 在此示例中，使用了 STDPREFIX。 有关 STDPREFIX 的可用值，请参阅 [如何实现更改每个跟踪行的前缀输出？](how-do-i-change-the-prefix-output-on-every-trace-line-.md)

<span id="USESUFFIX"></span><span id="usesuffix"></span>**USESUFFIX**  
定义要在记录事件时使用的后缀格式字符串。

<span id="FUNC"></span><span id="func"></span>**求**  
定义 trace 函数的名称和签名。 在此示例中，函数采用一个参数，而不采用格式字符串。

有关 Trace-If 表达式的另一个示例，请参阅 [如何实现在 C/c + + 宏中包含跟踪语句？](how-do-i-include-a-trace-statement-in-a-c-c---macro-.md) 一节。









