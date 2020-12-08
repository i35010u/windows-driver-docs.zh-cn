---
title: 如何实现向跟踪消息添加前缀和后缀
description: 如何实现向跟踪消息添加前缀和后缀
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1bb8790e01859f59d17b19ba711c48b02e04c4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831545"
---
# <a name="how-do-i-add-a-prefix-and-suffix-to-a-trace-message"></a>如何将前缀和后缀添加到跟踪消息？


您可以使用 [WPP 预处理器](wpp-preprocessor.md) 配置块向跟踪消息添加数据。

WPP 配置块由您在源代码中放置的 **begin \_ wpp config** 和 **end \_ wpp** 语句定义。

**开始 \_ wpp 配置**

...

*配置块*

...

**结束 \_ wpp**

如果将配置数据放在标头文件中，请在项目属性 (为 **WPP 跟踪**) 指定标头文件的名称。 在 "属性" 页上的 " **文件选项** " 下，指定 **扫描配置文件**。 有关详细信息，请参阅 [WPP 预处理器](wpp-preprocessor.md) 。

### <a name="span-idconfiguration_block_syntaxspanspan-idconfiguration_block_syntaxspanconfiguration-block-syntax"></a><span id="configuration_block_syntax"></span><span id="CONFIGURATION_BLOCK_SYNTAX"></span>配置块语法

<span id="__USEPREFIX__Function_Name___Format_string___"></span><span id="__useprefix__function_name___format_string___"></span><span id="__USEPREFIX__FUNCTION_NAME___FORMAT_STRING___"></span>**//USEPREFIX (**<em>函数 \_ 名称</em>**，"**<em>格式字符串</em>**" ) ;**  
定义要在记录事件时使用的格式字符串前缀。 第一个参数是此前缀所应用到的函数的名称。 第二个参数是要使用的格式字符串。 若要使用默认值，请指定%！STDPREFIX!. 默认跟踪消息前缀指定 CPU 号、进程 ID、线程 ID、时间戳（采用协调世界时） (UTC) 格式和控件 GUID 友好名称。

```
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
```

<span id="__FUNC_Function_Name_args__EXP__"></span><span id="__func_function_name_args__exp__"></span><span id="__FUNC_FUNCTION_NAME_ARGS__EXP__"></span>**//FUNC** *函数 \_ 名称*{*args*} (EXP) **;**  
定义 trace 函数的名称和签名。 使用大括号 **{}** 定义函数的设置值。 在下面的示例中，函数采用一个参数，而不采用格式字符串，并且级别设置为 "错误"。

```
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
```

<span id="__USESUFFIX__Function_Name___Format_string___"></span><span id="__usesuffix__function_name___format_string___"></span><span id="__USESUFFIX__FUNCTION_NAME___FORMAT_STRING___"></span>**//USESUFFIX (**<em>函数 \_ 名称</em>**，"**<em>格式字符串</em>**" ) ;**  
定义要在记录事件时使用的格式字符串后缀。 第一个参数是此后缀应用到的函数的名称。 第二个参数是要使用的格式字符串。 您可以在代码中使用变量名。

```
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
```

### <a name="span-idexample_configuration_blockspanspan-idexample_configuration_blockspanexample-configuration-block"></a><span id="example_configuration_block"></span><span id="EXAMPLE_CONFIGURATION_BLOCK"></span>示例配置块

下面的示例定义了一个跟踪宏，该宏使用格式字符串前缀和后缀。 如果正在定义跟踪宏，还必须定义宏以选择记录器，并检查是否应记录事件。

```
//MACRO: TRACE_RETURN
//
//begin_wpp config
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
//end_wpp

//
// The next two macros are for checking if the event should be logged, and for
// choosing the logger handle to use when calling the ETW trace API
//
#define WPP_LEVEL_EXP_ENABLED(LEVEL, HR) WPP_FLAG_ENABLED(LEVEL)
#define WPP_LEVEL_EXP_LOGGER(LEVEL, HR) WPP_FLAG_LOGGER(LEVEL)
```

### <a name="span-idexample_trace_resultsspanspan-idexample_trace_resultsspanexample-trace-results"></a><span id="example_trace_results"></span><span id="EXAMPLE_TRACE_RESULTS"></span>跟踪结果示例

```
[0]0F78.0460::06/24/2006-15:54:54.880 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
```

 

 





