---
title: 如何为跟踪消息添加前缀和后缀
description: 如何为跟踪消息添加前缀和后缀
ms.assetid: d8cd0a90-d020-4b1e-bec1-7d920964169e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e6c99def3fd22b8a4f8ef2733a6785022c11491
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359494"
---
# <a name="how-do-i-add-a-prefix-and-suffix-to-a-trace-message"></a>如何将前缀和后缀添加到跟踪消息？


可以使用[WPP 预处理器](wpp-preprocessor.md)配置块，将数据添加到跟踪消息。

由定义 WPP 配置块**开始\_wpp config**和**最终\_wpp**放置在源代码中的语句。

**//begin\_wpp config**

...

*配置块*

...

**//end\_wpp**

如果标头文件中将配置数据，在项目属性中指定的标头文件名称 (对于**WPP 跟踪**)。 下**文件选项**在属性页上，指定**扫描配置文件**。 请参阅[WPP 预处理器](wpp-preprocessor.md)有关详细信息。

### <a name="span-idconfigurationblocksyntaxspanspan-idconfigurationblocksyntaxspanconfiguration-block-syntax"></a><span id="configuration_block_syntax"></span><span id="CONFIGURATION_BLOCK_SYNTAX"></span>配置块语法

<span id="__USEPREFIX__Function_Name___Format_string___"></span><span id="__useprefix__function_name___format_string___"></span><span id="__USEPREFIX__FUNCTION_NAME___FORMAT_STRING___"></span>**USEPREFIX (**<em>函数\_名称</em>**，"**<em>格式字符串</em>**");**  
定义要记录的事件时使用的格式字符串前缀。 第一个参数是函数的此前缀适用的名称。 第二个参数是要使用的格式字符串。 若要使用的默认值，指定 %！STDPREFIX ！。 默认跟踪消息前缀指定 CPU 数量、 进程 ID、 线程 ID、 协调世界时 (UTC) 格式的时间戳和控制 GUID 友好名称。

```
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
```

<span id="__FUNC_Function_Name_args__EXP__"></span><span id="__func_function_name_args__exp__"></span><span id="__FUNC_FUNCTION_NAME_ARGS__EXP__"></span>**//FUNC** *Function\_Name*{*args*}(EXP)**;**  
定义的名称和跟踪函数的签名。 大括号 **{}** 用于定义集值函数。 在以下示例中，该函数采用一个参数和没有任何格式字符串，和的级别设置为错误。

```
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
```

<span id="__USESUFFIX__Function_Name___Format_string___"></span><span id="__usesuffix__function_name___format_string___"></span><span id="__USESUFFIX__FUNCTION_NAME___FORMAT_STRING___"></span>**USESUFFIX (**<em>函数\_名称</em>**，"**<em>格式字符串</em>**");**  
定义要记录的事件时使用的格式字符串后缀。 第一个参数是函数的应用于此后缀的名称。 第二个参数是要使用的格式字符串。 可以在代码中使用变量名称。

```
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
```

### <a name="span-idexampleconfigurationblockspanspan-idexampleconfigurationblockspanexample-configuration-block"></a><span id="example_configuration_block"></span><span id="EXAMPLE_CONFIGURATION_BLOCK"></span>示例配置块

下面的示例定义一个跟踪宏，使用格式字符串作为前缀和后缀。 如果要定义跟踪宏，您还必须定义宏来选择记录器，并检查是否应记录该事件。

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

### <a name="span-idexampletraceresultsspanspan-idexampletraceresultsspanexample-trace-results"></a><span id="example_trace_results"></span><span id="EXAMPLE_TRACE_RESULTS"></span>示例跟踪结果

```
[0]0F78.0460::06/24/2006-15:54:54.880 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
```

 

 





