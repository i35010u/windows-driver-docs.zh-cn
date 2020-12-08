---
title: JavaScript 扩展中的本机调试器对象 - 类型对象
description: 本机调试器对象表示调试器环境的各种构造。 JavaScript 扩展可以直接访问基础语言的类型系统。 此访问通过类型对象的概念来表示。
ms.date: 01/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: ae21c41ff404b3c8c185d401057f3660dfff0faf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836993"
---
# <a name="native-debugger-objects-in-javascript-extensions---type-objects"></a>JavaScript 扩展中的本机调试器对象 - 类型对象

 本机调试器对象表示调试器环境的各种构造。 JavaScript 扩展可以直接访问基础语言的类型系统。 此访问通过 *类型对象* 的概念来表示。 本主题介绍与类型对象相关联的属性。

本机调试器对象表示调试器环境的各种构造和行为。 对象可以传递到 (中，也可以在) JavaScript 扩展中获取，以操作调试器的状态。

有关调试器对象 JavaScript 扩展的信息，请参阅 [Javascript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

有关使用 JavaScript 的常规信息，请参阅 [Javascript 调试器脚本](javascript-debugger-scripting.md)。

## <a name="type-objects"></a>类型对象

可以通过多种方式获取类型对象：

- 从对象：如果脚本在 JavaScript 中有本机对象，则可以对该对象访问 *targetType* 属性，以便获取表示本机对象的静态类型的 *类型对象* 。
- 从主机：可以调用 *getModuleType* API，以便为特定模块中定义的任何类型返回 *类型对象* 。

获取类型对象后，它将具有以下属性：

<table>
<tr><td><b>名称</b></td><td><b>Signature</b></td><td><b>说明</b></td></tr>

<tr><td>name</td><td>properties</td><td>返回类型的名称。</td></tr>

<tr><td>大小</td><td>properties</td><td>将类型的大小返回为64位值。</td></tr>

<tr><td>typeKind</td><td>properties</td><td>将类型的类型作为字符串返回。  这可以是以下值之一： "udt"、"指针"、"memberPointer"、"array"、"function"、"typedef"、"枚举" 或 "内部"。</td></tr>

<tr><td>baseType</td><td>properties</td><td>返回此类型所基于的类型的类型对象。  这不表示 c + + 继承。  对于指针类型，这是指向的内容的类型。  对于数组类型，这是数组中包含的类型。</td></tr>

<tr><td>fields</td><td>properties</td><td>返回一个对象，该对象具有可作为命名属性访问的类型的所有命名字段。  每个属性的值是一个 <i>字段对象</i> ，如下所述。</td></tr>

<tr><td>baseClasses</td><td>properties</td><td>返回该类型的所有直接基类的数组。  数组中的每个对象都是一个 <i>基类对象</i> ，如下所述。</td></tr>

<tr><td>functionReturnType</td><td>properties</td><td>对于函数类型，这将返回表示函数的返回类型的类型对象。</td></tr>

<tr><td>functionParameterTypes</td><td>properties</td><td>对于函数类型，这会返回类型对象的数组，这些对象表示函数的参数类型。</td></tr>

<tr><td>functionCallingConvention</td><td>properties</td><td>对于函数类型，这会将函数的调用约定作为字符串返回。  这可以是以下值之一： "unknown"、"__cdecl"、"fastcall"、"stdcall" 或 "thiscall"。</td></tr>

<tr><td>pointerKind</td><td>properties</td><td>对于指针类型，这会将指针的类型作为字符串返回。  这可以是以下值之一： "standard"、"reference"、"rValueReference" 或 "cxHat"。</td></tr>

<tr><td>memberType</td><td>properties</td><td>对于作为成员指针的指针类型，这将返回表示 member 类的类型对象。</td></tr>

<tr><td>isGeneric</td><td>properties</td><td>返回该类型是否为泛型。  对于模板类型，这将返回 true。</td></tr>

<tr><td>genericArguments</td><td>properties</td><td>对于泛型类型，这将返回泛型参数的数组。  此类参数可以是类型参数，也可以是常量值。</td></tr>

<tr><td>isBitField</td><td>properties</td><td>返回该类型的存储是否为位域。</td></tr>

<tr><td>bitFieldPositions</td><td>properties</td><td>对于表示域存储的类型，这将返回一个位域说明类型，指示位域的位置。</td></tr>

</table>

所有这些项都在阶段2初始化期间存在。

## <a name="field-objects"></a>字段对象

类型中的每个字段都由一个字段对象描述，该字段对象的属性如下所示：

<table>

<tr><td><b>名称</b></td><td><b>Signature</b></td><td><b>说明</b></td></tr>

<tr><td>name</td><td>properties</td><td>返回字段的名称。</td></tr>

<tr><td>type</td><td>properties</td><td>返回表示字段的静态类型的类型对象。</td></tr>

<tr><td>locationKind</td><td>properties</td><td>将字段 (存储) 的位置类型作为字符串返回。  这可以是以下值之一： "member"、"static"、"常量" 或 "none"。</td></tr>

<tr><td>offset</td><td>properties</td><td>对于其位置类型指示偏移量的字段 (例如： "member" ) ，这会将字段在其包含类型内的偏移量返回为64位值。</td></tr>

<tr><td>location</td><td>properties</td><td>对于其位置类型指示位置 (（例如： "static" ) ）的字段，这会将字段位置作为 <i>location 对象返回。</i></td></tr>

<tr><td>值</td><td>properties</td><td>对于其位置种类指示值的字段 (例如： "常量" ) ，这将返回字段的值。</td></tr>

</table>

所有这些项都在阶段2初始化期间存在。

## <a name="base-class-objects"></a>基类对象

类型中的每个基类都由具有如下属性的基类对象描述：

<table>

<tr><td><b>名称</b></td><td><b>Signature</b></td><td><b>说明</b></td></tr>

<tr><td>name</td><td>properties</td><td>返回基类的名称。</td></tr>

<tr><td>offset</td><td>properties</td><td>返回此基类在其包含类型内的偏移量。</td></tr>

<tr><td>type</td><td>properties</td><td>返回表示基类的静态类型的类型对象。</td></tr>

</table>

所有这些项都在阶段2初始化期间存在。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)

[JavaScript 扩展中的本机调试器对象-设计和测试注意事项](native-objects-in-javascript-extensions-design-considerations.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)
