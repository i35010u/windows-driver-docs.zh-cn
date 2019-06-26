---
title: 可以自定义 DoTraceMessage
description: 可以自定义 DoTraceMessage
ms.assetid: 4c5c4990-6095-4ab8-a20b-7597b3169f52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63dbeae90a2de439ad3f26d58ef95bc0e6dfe139
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371625"
---
# <a name="can-i-customize-dotracemessage"></a>是否可以自定义 DoTraceMessage？


是的您可以编写自己的版本[ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏。 DoTraceMessage 生成的跟踪消息。

[TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)示例驱动程序提供了本主题中所述的方法的示例。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

### <a name="span-iddotracemessagedefaultversionspanspan-iddotracemessagedefaultversionspandotracemessage-default-version"></a><span id="dotracemessage__default_version"></span><span id="DOTRACEMESSAGE__DEFAULT_VERSION"></span>DoTraceMessage:默认版本

默认情况下，DoTraceMessage 宏采用以下格式：

```
DoTraceMessage(Flag,"Message",MessageVariables...);
```

在此默认版本，*标志*表示[跟踪标志](trace-flags.md)，这是在其下生成的消息的条件。 *MessageVariables*包含驱动程序定义，并在跟踪消息中都出现的变量的以逗号分隔列表。 *MessageVariables*使用格式化变量**printf**元素。 预处理器 WPP 从 DoTraceMessage 宏创建的编译器指令。 此宏会将消息定义信息和格式设置信息添加到为其生成的 PDB 文件[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。

DoTraceMessage 宏将展开，在逻辑上，为以下：

```
PRE macro // If defined
If (WPP_CHECK_INIT && Flag is enabled) {
 ....Call WmiTraceMessage;
}
POST macro // If defined
```

请考虑下面的代码示例。

```
DoTraceMessage(ERROR, "IOCTL = %d", ControlCode);
```

此调用时启用错误标志，则生成的跟踪消息。 该消息是"IOCTL = %d"和*MessageVariables*的值*ControlCode*。

如果定义了预日志记录和后的日志记录宏，它们也将得到扩展。 在 Microsoft Windows 2000 和更高版本操作系统支持预宏和 POST 宏。 若要使用宏，必须使用 WDK 构建该驱动程序。 如果使用早期版本的 Windows 驱动程序开发工具包 (DDK) 生成一个驱动程序，PRE 和 POST 功能不可用，并且宏将不会作为跟踪语句的一部分运行。 使用早期版本的 Windows DDK 构建该驱动程序可能不会导致生成中断，但该代码将无法按预期工作。

### <a name="span-iddotracemessagegeneralformatspanspan-iddotracemessagegeneralformatspandotracemessage-general-format"></a><span id="dotracemessage__general_format"></span><span id="DOTRACEMESSAGE__GENERAL_FORMAT"></span>DoTraceMessage:常规格式

下面是有效的跟踪消息函数的常规格式：

```
FunctionName(Conditions...,"Message",MessageVariables...);
```

显示的消息之前的参数被解释为条件。 该消息后显示的参数被解释为消息变量。

*条件*是以逗号分隔值的列表。 仅当满足所有条件都时生成的跟踪消息。 可以指定代码中支持任何条件。

### <a name="span-idexamplemytracespanspan-idexamplemytracespanexample-mytrace"></a><span id="example__mytrace"></span><span id="EXAMPLE__MYTRACE"></span>示例：MyTrace

下面是跟踪功能的示例。 此示例将跟踪级别和提供程序生成的跟踪消息的子组件的条件。

```
MyDoTrace(Level, Flag, Subcomponent,"Message",MessageVariables...);
```

例如：

```
MyDoTrace(TRACE_LEVEL_ERROR, VERBOSE, Network,"IOCTL = %d", ControlCode);
```

跟踪级别为 Evntrace.h，WDK 的 Include 子目录中的公共标头文件中定义的标准级别。

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

### <a name="span-idhowtocreateacustomtracingfunctionspanspan-idhowtocreateacustomtracingfunctionspanhow-to-create-a-custom-tracing-function"></a><span id="how_to_create_a_custom_tracing_function"></span><span id="HOW_TO_CREATE_A_CUSTOM_TRACING_FUNCTION"></span>如何创建自定义跟踪函数

若要创建的自定义跟踪功能，请执行以下步骤：

-   编写支持 DoTraceMessage 宏的宏的替代版本。

-   添加 **-func**参数运行\_WPP WPP 预处理器将调用的语句。

### <a name="span-idwritecustommacrosspanspan-idwritecustommacrosspanwrite-custom-macros"></a><span id="write_custom_macros"></span><span id="WRITE_CUSTOM_MACROS"></span>编写自定义的宏

若要创建更改的条件跟踪消息 （在消息之前显示的参数） 的自定义跟踪功能，必须编写备用版本支持跟踪函数的宏**WPP\_级别\_已启用**并**WPP\_级别\_记录器**。

-   **WPP\_级别\_已启用 (*标志*)** 确定是否使用指定的标志值启用日志记录。 它将返回 **，则返回 TRUE**或**FALSE**。

-   **WPP\_级别\_记录器 (*标志*)** 查找跟踪会话向其提供程序，并返回到跟踪会话的句柄。

例如，如果你想要包括的跟踪级别，除了标志，作为一项条件，定义新 WPP\_级别\_包括跟踪级别的已启用宏。 可以基于新的宏的定义默认宏，如以下代码示例所示。

```
#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >=lvl
```

通常情况下，WPP\_级别\_记录器宏不会受到影响。 在这些情况下，可以定义新的宏是默认宏。 例如：

```
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) WPP_LEVEL_LOGGER(flags)
```

但是，在某些情况下，您需要更改记录器宏。 例如，你可能想要编写取决于仅跟踪级别以及不在标志上的跟踪功能。

在下面的代码示例中，在宏中标志值将替换为虚拟值。 声明控制 GUID 定义时不定义任何标志。

```
#define WPP_CONTROL_GUIDS \
   WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(DUMMY))
```

```
#define WPP_LEVEL_LOGGER(lvl) (WPP_CONTROL(WPP_BIT_ ## DUMMY).Logger)
```

### <a name="span-idaddthefunctiontowppspanspan-idaddthefunctiontowppspanadd-the-function-to-wpp"></a><span id="add_the_function_to_wpp"></span><span id="ADD_THE_FUNCTION_TO_WPP"></span>此函数添加到 WPP

若要将自定义跟踪功能添加到 WPP，添加 **-func**参数运行\_WPP 语句与声明的函数，如下面的代码示例显示了。

```
RUN_WPP=$(SOURCES) -km -func:DoTraceLevelMessage(LEVEL,FLAGS,MSG,...)
```

**请注意**您必须指定**公里**运行中切换\_WPP 指令用于用户模式应用程序或动态链接库 (Dll)。



有关运行的可选参数的完整列表\_WPP，请参阅[WPP 预处理器](wpp-preprocessor.md)。









