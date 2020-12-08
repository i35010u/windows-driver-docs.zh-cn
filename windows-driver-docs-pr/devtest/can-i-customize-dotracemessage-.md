---
title: 能否自定义 DoTraceMessage
description: 能否自定义 DoTraceMessage
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 823dbc5cead56f96bd24489bce76d954374fb15b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791589"
---
# <a name="can-i-customize-dotracemessage"></a>是否可以自定义 DoTraceMessage？


是的，您可以编写自己的 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 宏版本。 DoTraceMessage 生成跟踪消息。

[TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)示例驱动程序提供了本主题中描述的方法的示例。 GitHub 上的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中提供了[TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver) 。

### <a name="span-iddotracemessage__default_versionspanspan-iddotracemessage__default_versionspandotracemessage-default-version"></a><span id="dotracemessage__default_version"></span><span id="DOTRACEMESSAGE__DEFAULT_VERSION"></span>DoTraceMessage：默认版本

默认情况下，DoTraceMessage 宏的格式如下：

```
DoTraceMessage(Flag,"Message",MessageVariables...);
```

在此默认版本中， *标志* 表示 [跟踪标志](trace-flags.md)，这是生成消息时所依据的条件。 *MessageVariables* 包含一个逗号分隔的变量列表，驱动程序将定义这些变量并将其显示在跟踪消息中。 *MessageVariables* 变量使用 **printf** 元素进行格式设置。 WPP 预处理器从 DoTraceMessage 宏创建编译器指令。 此宏向为 [跟踪提供程序](trace-provider.md)生成的 PDB 文件添加消息定义信息和格式设置信息，例如内核模式驱动程序或用户模式应用程序。

DoTraceMessage 宏按逻辑展开为以下内容：

```
PRE macro // If defined
If (WPP_CHECK_INIT && Flag is enabled) {
 ....Call WmiTraceMessage;
}
POST macro // If defined
```

请考虑以下代码示例。

```
DoTraceMessage(ERROR, "IOCTL = %d", ControlCode);
```

启用错误标志后，此调用会生成跟踪消息。 消息为 "IOCTL =% d"， *MessageVariables* 是 *ControlCode* 的值。

如果预日志记录和日志记录后的宏已定义，则它们也将展开。 Microsoft Windows 2000 及更高版本的操作系统支持宏和发布宏。 若要使用宏，必须使用 WDK 构建驱动程序。 如果使用早期版本的 Windows 驱动程序开发工具包生成驱动程序 (的 DDK) ，则 PRE 和 POST 功能不可用，并且宏将不会作为跟踪语句的一部分运行。 使用早期版本的 Windows DDK 构建驱动程序可能不会导致生成中断，但代码不会按预期方式工作。

### <a name="span-iddotracemessage__general_formatspanspan-iddotracemessage__general_formatspandotracemessage-general-format"></a><span id="dotracemessage__general_format"></span><span id="DOTRACEMESSAGE__GENERAL_FORMAT"></span>DoTraceMessage：常规格式

下面是有效的跟踪消息函数的常规格式：

```
FunctionName(Conditions...,"Message",MessageVariables...);
```

消息之前显示的参数被解释为条件。 消息后显示的参数被解释为消息变量。

*条件* 是以逗号分隔的值列表。 仅当所有条件均为 true 时，才生成跟踪消息。 您可以指定代码中支持的任何条件。

### <a name="span-idexample__mytracespanspan-idexample__mytracespanexample-mytrace"></a><span id="example__mytrace"></span><span id="EXAMPLE__MYTRACE"></span>示例： MyTrace

下面是一个跟踪函数的示例。 此示例为生成跟踪消息的提供程序的跟踪级别和子组件添加条件。

```
MyDoTrace(Level, Flag, Subcomponent,"Message",MessageVariables...);
```

例如：

```
MyDoTrace(TRACE_LEVEL_ERROR, VERBOSE, Network,"IOCTL = %d", ControlCode);
```

跟踪级别是在 Evntrace 中定义的标准级别，它是在 WDK 的包含子目录中的公共标头文件。

```
#define TRACE_LEVEL_NONE        0   // Tracing is not on
#define TRACE_LEVEL_FATAL       1   // Abnormal exit or termination
#define TRACE_LEVEL_ERROR       2   // Severe errors that need logging
#define TRACE_LEVEL_WARNING     3   // Warnings such as allocation failure
#define TRACE_LEVEL_INFORMATION 4   // Includes non-error cases(for example, Entry-Exit)
#define TRACE_LEVEL_VERBOSE     5   // Detailed traces from intermediate steps
#define TRACE_LEVEL_RESERVED6   6
#define TRACE_LEVEL_RESERVED7   7
#define TRACE_LEVEL_RESERVED8   8
#define TRACE_LEVEL_RESERVED9   9
```

### <a name="span-idhow_to_create_a_custom_tracing_functionspanspan-idhow_to_create_a_custom_tracing_functionspanhow-to-create-a-custom-tracing-function"></a><span id="how_to_create_a_custom_tracing_function"></span><span id="HOW_TO_CREATE_A_CUSTOM_TRACING_FUNCTION"></span>如何创建自定义跟踪函数

若要创建自定义跟踪功能，请执行以下步骤：

-   编写支持 DoTraceMessage 宏的其他版本的宏。

-   将 **-func** 参数添加到 \_ 调用 wpp 预处理器的 RUN WPP 语句中。

### <a name="span-idwrite_custom_macrosspanspan-idwrite_custom_macrosspanwrite-custom-macros"></a><span id="write_custom_macros"></span><span id="WRITE_CUSTOM_MACROS"></span>编写自定义宏

若要创建一个自定义跟踪函数，该函数将 (消息) 之前出现的参数更改跟踪消息的条件，则必须编写支持跟踪函数的其他版本的宏， **启用 wpp \_ 级别 \_** 和 **wpp \_ 级别 \_ 记录器**。

-   **WPP \_\_启用了级别 (*标志*)** 确定是否已启用具有指定标志值的日志记录。 它返回 **TRUE** 或 **FALSE**。

-   **WPP \_级别 \_ 记录器 (*标志*)** 查找启用了提供程序的跟踪会话并为跟踪会话返回一个句柄。

例如，如果你想要包含跟踪级别，则除了标志以外，还需要定义一个包含跟踪级别的新的 \_ 启用 WPP 级别的 \_ 宏。 可以将新宏的定义基于默认宏，如下面的代码示例所示。

```
#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >=lvl
```

通常，WPP \_ 级别 \_ 记录器宏不受影响。 在这些情况下，可以将新宏定义为默认宏。 例如：

```
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) WPP_LEVEL_LOGGER(flags)
```

但是，在某些情况下，需要更改记录器宏。 例如，你可能希望编写一个仅依赖于跟踪级别而不依赖于标志的跟踪函数。

在下面的代码示例中，宏中的 flags 值被替换为一个虚拟值。 在声明控件 GUID 定义时不定义任何标志。

```
#define WPP_CONTROL_GUIDS \
   WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(DUMMY))
```

```
#define WPP_LEVEL_LOGGER(lvl) (WPP_CONTROL(WPP_BIT_ ## DUMMY).Logger)
```

### <a name="span-idadd_the_function_to_wppspanspan-idadd_the_function_to_wppspanadd-the-function-to-wpp"></a><span id="add_the_function_to_wpp"></span><span id="ADD_THE_FUNCTION_TO_WPP"></span>将函数添加到 WPP

若要将自定义跟踪函数添加到 WPP，请使用函数的声明将 **-func** 参数添加到 RUN \_ WPP 语句，如下面的代码示例所示。

```
RUN_WPP=$(SOURCES) -km -func:DoTraceLevelMessage(LEVEL,FLAGS,MSG,...)
```

**注意**  不能在用户模式应用程序或动态链接库的 "运行 WPP" 指令中指定 **-公里** 开关 \_ (dll) 。



有关运行 WPP 的可选参数的完整列表 \_ ，请参阅 [WPP 预处理器](wpp-preprocessor.md)。
