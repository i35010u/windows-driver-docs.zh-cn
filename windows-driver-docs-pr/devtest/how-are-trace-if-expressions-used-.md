---
title: 如何将跟踪-如果使用表达式
description: 如何将跟踪-如果使用表达式
ms.assetid: 05fc8225-ba4e-4718-a5e1-c9e49ec931b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b68ac23817724130314ed08d04950621e896f75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543917"
---
# <a name="how-are-trace-if-expressions-used"></a>如何将跟踪-如果使用表达式？


若要帮助你了解如何跟踪-如果使用了表达式，我们提供了演示如何使用此类表达式的示例和语法的"开始\_wpp config"语句。 此示例中引用的函数跟踪\_返回，该记录的事件，如果表达式 FAILED(HR) 为 true。

FAILED(HR) 为 true，如果假定没有有状态 ULONG 的源文件，并将通过调用跟踪记录一个事件\_RETURN(Status)。
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

在前面的示例，请注意，、 跟踪\_之间开始新的定义返回\_wpp 配置和结束\_wpp 行。 此定义然后跟预 / 宏和已启用和记录器定义发布到发布。

在 begin\_wpp 配置和结束\_wpp 分隔符定义分析由预处理器配置块。 包含配置块定义的文件必须由 WPP 扫描。 使用-scan:file.extension 参数指定此文件。

**请注意**璝惠 **-扫描**和其他**运行\_WPP**选项，请参阅[WPP 预处理器](wpp-preprocessor.md)。



以下列表提供了有关示例配置块中的每个语句的详细信息：

<span id="USEPREFIX"></span><span id="useprefix"></span>**USEPREFIX**  
定义要记录的事件时使用的前缀格式字符串。 在示例中，使用 STDPREFIX。 适用于 STDPREFIX 的值，请参阅[如何更改跟踪的每个行上的前缀输出？](how-do-i-change-the-prefix-output-on-every-trace-line-.md)

<span id="USESUFFIX"></span><span id="usesuffix"></span>**USESUFFIX**  
定义要记录的事件时使用的后缀格式字符串。

<span id="FUNC"></span><span id="func"></span>**FUNC**  
定义名称和跟踪函数的签名。 在示例中，该函数采用一个参数和没有任何格式字符串。

有关跟踪的另一个示例-如果表达式，请参阅[如何将跟踪语句包括中的 C/c + + 宏？](how-do-i-include-a-trace-statement-in-a-c-c---macro-.md)部分。









