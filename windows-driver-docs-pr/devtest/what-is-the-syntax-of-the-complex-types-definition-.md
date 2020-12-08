---
title: 复杂类型定义的语法是什么
description: 复杂类型定义的语法是什么
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed495178b28ec5cbdc068d511c11012768dba130
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810699"
---
# <a name="what-is-the-syntax-of-the-complex-types-definition"></a>复杂类型定义的语法是什么？


Windows (ETW) 的事件跟踪定义了用于跟踪函数的几个简单和复杂类型。 这些类型在 Defaultwpp.ini 文件中声明。 不过，你可以创建自己的自定义配置文件，并指示 WPP 使用该文件。

复杂数据类型定义 CPLX 类型的格式如下所示 \_ \_ ：

```
DEFINE_CPLX_TYPE(TypeName, HelperMacroName, ArgumentType, WppMofType,"WppMofFormat", TypeSignature, Priority, Slots);
```

例如：

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

### <a name="span-idformat_elementsspanspan-idformat_elementsspanformat-elements"></a><span id="format_elements"></span><span id="FORMAT_ELEMENTS"></span>格式元素

<span id="TypeName"></span><span id="typename"></span><span id="TYPENAME"></span>*TypeName*  
WPP 使用此字段来标识复杂类型。 例如， **。 \*ls**。

<span id="HelperMacroName"></span><span id="helpermacroname"></span><span id="HELPERMACRONAME"></span>*HelperMacroName*  
一个帮助器宏，它以长度/地址对的格式将参数转换为可变长度数组。 **TraceMessage** 函数需要此格式的变量参数列表中的每个条目。

若要正确设置参数的格式，必须在 helper 宏的定义中使用 [**WPP \_ LOGPAIR**](/previous-versions/windows/hardware/previsioning-framework/ff556197(v=vs.85)) 宏，如以下示例中所示：

```
#define HelperMacroName(x) WPP_LOGPAIR(length, x)
```

**注意**  根据要实现的跟踪逻辑，可能需要使用多个 WPP LOGPAIR 宏来定义宏 \_ 。

 

<span id="Argument_Type"></span><span id="argument_type"></span><span id="ARGUMENT_TYPE"></span>*参数类型*  
指示 *TypeName* 类型的参数可以接受的值。 例如， **const xwcs \_ t&**。

<span id="WppMofType"></span><span id="wppmoftype"></span><span id="WPPMOFTYPE"></span>*WppMofType*  
指定 WPP 预处理器可识别的托管对象格式 (MOF) 类型

<span id="WppMofFormat"></span><span id="wppmofformat"></span><span id="WPPMOFFORMAT"></span>*WppMofFormat*  
指定 WPP 预处理器可识别的格式说明符，如 **"s"**。

<span id="TypeSignature"></span><span id="typesignature"></span><span id="TYPESIGNATURE"></span>*TypeSignature*  
追加到函数名称的字符串，用于将它与复杂类型相关联。 下划线之间必须有一个或多个字符。 例如， **\_ xwcs \_ t \_**。

<span id="Priority"></span><span id="priority"></span><span id="PRIORITY"></span>*大事*  
此元素是保留元素，且必须设置为零。

<span id="Slots"></span><span id="slots"></span><span id="SLOTS"></span>*槽*  
指定 WPP 预处理器向此复杂类型的 [TraceMessage](/windows/win32/api/evntrace/nf-evntrace-tracemessage) 函数传递的可变长度参数的最大数目。 此 format 元素是可选的。 如果未指定此元素，则 WPP 使用默认值1。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

若要定义复杂类型，请执行以下操作：

1.  创建本地配置文件。 此文件应包含定义 \_ 复杂类型的定义 CPLX \_ 类型的宏。

2.  指定 [WPP 预处理器](wpp-preprocessor.md)的本地配置文件。 打开项目属性。 在 " **WPP 跟踪**、 **文件选项**" 下，使用 " **其他配置文件** " 字段指定配置文件 (**-ini** 参数) 的名称。 请确保启用 WPP 跟踪，方法是将 " **运行 Wpp** " 设置为 **"是"**。 有关详细信息，请参阅 WPP 预处理器。

例如，可以创建一个本地配置文件 ( # A0) ，该文件定义一个名为的复杂类型 **。 \*ls**。 可以通过以下方式定义复杂类型：

```
DEFINE_CPLX_TYPE(.*ls, WPP_LOGXWCS, const xwcs_t&, ItemPWString,"s", _xwcs_t_, 0, 2);
```

然后，当 WPP 查看类型时 **。 \*ls**，如中：

```
printf("my string is %.*ls", value);
```

WPP 生成以下暂存函数 (其中 **SF** 表示 "暂存函数" ) ：

```
WPP_SF__xwcs_t_(..., const xwcs_t& a1) {
    TraceMessage(..., WPP_LOGXWCS(a1) 0);
}
```

然后，WPP 生成 MOF 条目，如以下字符串中的 **。 \*ls** 类型名称被替换为适当的 MOF 格式 **% s**。

```
"my string is %s"
{
    Value, ItemPWString
}
```

它还会生成类型的结构，如

```
struct xwcs_t {
      WCHAR*    _buf;
      short     _len;
      xwcs_t(short buf, short len):_buf(buf),_len(len){}
};
```

现在，添加一个宏，将数据类型组合为 **xwstr \_ t** 类型的字符串，如下所示：

```
#define WPP_LOGXWCS(x) WPP_LOGPAIR(2, &(x)._len) WPP_LOGPAIR((x)._len, (x)._buf)
```

其中， **ItemPWString** 是 WPP 识别的计数 Unicode 字符串类型。 长度指定为2个字节。

当 ETW 解释 WPP \_ LOGXWCS 定义时，它会将一个2字节的字符串放入缓冲区，并解释第一个 [**WPP \_ LOGPAIR**](/previous-versions/windows/hardware/previsioning-framework/ff556197(v=vs.85)) 宏。 Etw 在 ETW 解释第二个 WPP LOGPAIR 宏时，将该字符串的所有字节复制到缓冲区 \_ 中。

由于你指定了与数据分隔的长度，因此 WPP \_ LOGXWCS 将使用两个 [TraceMessage](/windows/win32/api/evntrace/nf-evntrace-tracemessage)槽。 因此，数字 **2** 是第8个参数。

调用 [WPP 预处理器](wpp-preprocessor.md)时，使用 " **忽略感叹号** " 选项 (**-noshrieks**) 。 这有助于 WPP 识别名称的复杂类型，该类型的名称未用惊叹号括起来 (！ ) ，也称为 "shrieks"。

有关 WPP 跟踪选项的完整列表以及如何从项目属性页设置这些选项的信息，请参阅 [Wpp 预处理器](wpp-preprocessor.md)。

 

