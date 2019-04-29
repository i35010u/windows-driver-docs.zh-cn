---
title: 复杂类型定义的语法是什么
description: 复杂类型定义的语法是什么
ms.assetid: c378839a-3714-4b4e-94a6-d3e1dcf8a610
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68dc7cce9f5340b4f4a7a47c9c7a7cdea228b681
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386362"
---
# <a name="what-is-the-syntax-of-the-complex-types-definition"></a>复杂类型定义的语法是什么？


Windows 事件跟踪 (ETW) 跟踪函数中定义使用的几个简单和复杂类型。 Defaultwpp.ini 文件中声明这些类型。 但是，可以创建自己的自定义配置文件，并直接 WPP 来使用它。

复杂数据类型定义的格式\_CPLX\_类型，如下所示：

```
DEFINE_CPLX_TYPE(TypeName, HelperMacroName, ArgumentType, WppMofType,"WppMofFormat", TypeSignature, Priority, Slots);
```

例如：

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

### <a name="span-idformatelementsspanspan-idformatelementsspanformat-elements"></a><span id="format_elements"></span><span id="FORMAT_ELEMENTS"></span>格式元素

<span id="TypeName"></span><span id="typename"></span><span id="TYPENAME"></span>*TypeName*  
WPP 使用此字段来标识的复杂类型。 例如， **。\*ls**。

<span id="HelperMacroName"></span><span id="helpermacroname"></span><span id="HELPERMACRONAME"></span>*HelperMacroName*  
帮助器宏参数转换为长度/地址对格式中的变长数组。 此格式所需**TraceMessage**其变量自变量列表中的项的每个函数。

若要正确设置参数的格式，必须使用[ **WPP\_LOGPAIR** ](https://msdn.microsoft.com/library/windows/hardware/ff556197)帮助器宏，如下面的示例中所示的定义中的宏：

```
#define HelperMacroName(x) WPP_LOGPAIR(length, x)
```

**请注意**  具体取决于您想要实现的跟踪逻辑，您可能需要定义宏通过使用多个 WPP\_LOGPAIR 宏。

 

<span id="Argument_Type"></span><span id="argument_type"></span><span id="ARGUMENT_TYPE"></span>*自变量类型*  
指示该参数的值*TypeName*可以接受类型。 例如， **const xwcs\_t &**。

<span id="WppMofType"></span><span id="wppmoftype"></span><span id="WPPMOFTYPE"></span>*WppMofType*  
指定的托管对象格式 (MOF) 类型的预处理器 WPP 识别

<span id="WppMofFormat"></span><span id="wppmofformat"></span><span id="WPPMOFFORMAT"></span>*WppMofFormat*  
指定一个格式说明符，例如 **"s"**，即由 WPP 预处理器识别。

<span id="TypeSignature"></span><span id="typesignature"></span><span id="TYPESIGNATURE"></span>*TypeSignature*  
一个字符串追加到要将它与复杂类型相关联的函数名称。 必须是单个字符或下划线之间的多个字符。 例如，  **\_xwcs\_t\_**。

<span id="Priority"></span><span id="priority"></span><span id="PRIORITY"></span>*优先级*  
此元素保留，并且必须设置为零。

<span id="Slots"></span><span id="slots"></span><span id="SLOTS"></span>*槽*  
指定 WPP 预处理器将传递给的变量长度参数的最大数目[TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)此复杂类型的函数。 此格式元素是可选的。 WPP 使用默认值为 1，如果未指定此元素。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

若要定义复杂类型，请执行以下操作：

1.  创建本地配置文件。 此文件应包含定义\_CPLX\_类型宏，用于定义复杂类型。

2.  指定的本地配置文件[WPP 预处理器](wpp-preprocessor.md)。 打开项目属性。 下**WPP 跟踪**，**文件选项**，使用**额外的配置文件**字段来指定配置文件的名称 (**-ini**参数)。 确保通过设置启用 WPP 跟踪**运行 WPP**到**是**。 有关详细信息，请参阅 WPP 预处理器。

例如，可以创建用于定义名为的复杂类型的本地配置文件 (Localwpp.ini) **。\*ls**。 按以下方式定义复杂类型：

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

然后，当 WPP 发现一种类型时，才 **。\*ls**，例如，在：

```
printf("my string is %.*ls", value);
```

WPP 生成以下临时函数 (其中**SF** "staging 函数"表示):

```
WPP_SF__xwcs_t_(..., const xwcs_t& a1) {
    TraceMessage(..., WPP_LOGXWCS(a1) 0);
}
```

WPP 然后生成一个 MOF 条目，例如以下字符串，其中 **。\*ls**类型名称替换为适当的 MOF 格式 **%s**。

```
"my string is %s"
{
    Value, ItemPWString
}
```

它还生成一个结构类型如

```
struct xwcs_t {
      WCHAR*    _buf;
      short     _len;
      xwcs_t(short buf, short len):_buf(buf),_len(len){}
};
```

现在，添加要合并的数据类型为类型字符串的宏**xwstr\_t**，按如下所示：

```
#define WPP_LOGXWCS(x) WPP_LOGPAIR(2, &(x)._len) WPP_LOGPAIR((x)._len, (x)._buf)
```

其中**ItemPWString** WPP 识别为计数 Unicode 字符串类型。 长度指定为 2 个字节。

当 ETW 解释 WPP\_LOGXWCS 定义，它将一个 2 字节的字符串放入第一个缓冲区[ **WPP\_LOGPAIR** ](https://msdn.microsoft.com/library/windows/hardware/ff556197)解释宏。 ETW 然后复制字符串的所有字节到缓冲区时 ETW 解释第二个 WPP\_LOGPAIR 宏

因为指定的长度不同于数据，WPP\_LOGXWCS 使用的两个槽[TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)。 因此，数字**2**是第 8 个参数。

调用时[WPP 预处理器](wpp-preprocessor.md)，使用**忽略感叹号**选项 (**-noshrieks**)。 这有助于 WPP 识别复杂类型具有名称未括在感叹号 （！），也称为"shrieks。"

WPP 跟踪选项以及有关如何从项目属性页中设置这些信息的完整列表，请参阅[WPP 预处理器](wpp-preprocessor.md)。

 

 





