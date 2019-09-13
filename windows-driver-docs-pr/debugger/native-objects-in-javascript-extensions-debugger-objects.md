---
title: JavaScript 扩展中的本机调试器对象 - 调试器对象详细信息
description: 本机调试器对象表示调试器环境的各种构造。 本主题介绍 JavaScript 扩展中的本机调试器对象的其他详细信息。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEE9
ms.date: 09/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 60b1790c42fe8cf05413c9ff64e891fb8c4eaf37
ms.sourcegitcommit: 3b7c8b3cb59031e0f4e39dac106c1598ad108828
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2019
ms.locfileid: "70935900"
---
# <a name="native-debugger-objects-in-javascript-extensions---debugger-object-details"></a>JavaScript 扩展中的本机调试器对象 - 调试器对象详细信息

本主题介绍有关使用 JavaScript 扩展中的本机调试器对象的其他详细信息。

本机调试器对象表示调试器环境的各种构造和行为。 对象可传递到 JavaScript 扩展中（或在中获取）以操作调试器的状态。

有关调试器对象 JavaScript 扩展的信息，请参阅[Javascript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

有关使用 JavaScript 的常规信息，请参阅[Javascript 调试器脚本](javascript-debugger-scripting.md)。

## <a name="span-iddebugger-objectsspanspan-iddebugger-objectsspanspan-iddebugger-objectsspandebugger-objects-in-javascript-extensions"></a><span id="Debugger-Objects"></span><span id="debugger-objects"></span><span id="DEBUGGER-OBJECTS"></span>JavaScript 扩展中的调试器对象

**传递本机对象**

可以通过多种方式在 JavaScript 扩展中传入或获取调试器对象。

-   可以将其传递给 JavaScript 函数或方法
-   它们可以是 JavaScript 原型的实例对象（例如可视化工具）
-   它们可从用于创建本机调试器对象的主机方法返回
-   它们可从用于创建调试器本机对象的主机方法返回

传递给 JavaScript 扩展的调试器对象具有此部分中描述的一组功能。

-   属性访问
-   投影名称
-   与本机调试器对象相关的特殊类型
-   其他属性

**属性访问**

尽管对象上存在一些属性，这些属性由 JavaScript 提供程序本身放置，但用于输入 JavaScript 的本机对象上的大多数属性都是由数据模型提供的。 这意味着，对于属性访问---对象名称或对象\[属性名称\]，将发生以下情况。

-   如果*属性名称是*由 JavaScript 提供程序自身投影到对象的属性的名称，则先将其解析为 this;本来
-   如果*propertyName*是由数据模型（另一个可视化工具）投影到对象的键的名称，则它将解析为此名称 second;本来
-   如果*propertyName*是本机对象的字段名称，则它将解析为第三个名称;本来
-   如果对象是指针，则将取消引用指针，以上的循环将继续（已取消引用的对象的投影属性，后跟一个后跟一个本地字段的键）

JavaScript 中的属性访问的常规方法--对象名称和对象\[属性名称\] --将访问对象的基础本机字段，与调试器中的 "dx" 命令非常相似。

**投影名称**

以下属性（和方法）投影到输入 JavaScript 的本机对象。

| 方法             | 签名                  | 描述                                                                                                                                |
|--------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| hostContext        | 属性                   | 返回一个对象，它表示对象中的上下文 (地址空间、 调试目标，等等...)                              |
| targetLocation     | 属性                   | 返回一个对象是一个抽象概念的其中对象是在地址空间内 (虚拟地址、 注册、 子寄存器，等等...) |
| targetSize         | 属性                   | 返回对象的大小（有效： sizeof （&lt;对象&gt;的类型）                                                                |
| addParentModel     | . addParentModel （object）    | 向对象添加新的父模型（类似于 JavaScript 原型，但位于数据型号端）                                          |
| removeParentModel  | . removeParentModel （object） | 从对象中移除给定的父模型                                                                                               |
| runtimeTypedObject | 属性                   | 对对象执行分析，并尝试将其转换为运行时（最常派生的）类型                                                 |

 

如果对象是指针，则将以下属性（和方法）投影到用于输入 JavaScript 的指针：

| 属性名 | 签名      | 描述                                                                    |
|---------------|----------------|--------------------------------------------------------------------------------|
| 添加           | 。添加（值）    | 在指针和指定的值之间执行指针数学加法运算     |
| 地址       | 属性       | 将指针的地址作为64位序号对象返回（库类型） |
| 取消引用   | 。取消引用（） | 取消引用指针并返回基础对象                     |
| IsNull        | 属性       | 返回指针值是否为 nullptr （0）                        |

 

**与本机调试器对象相关的特殊类型**

**位置对象**

从本机对象的 targetLocation 属性返回的 location 对象包含以下属性（和方法）。

| 属性名 | 签名        | 描述                                          |
|---------------|------------------|------------------------------------------------------|
| 添加           | 。添加（值）      | 向位置添加绝对字节偏移量。        |
| 减去      | . 减法（值） | 从位置减去绝对字节偏移量。 |

 

**其他属性**

**Iterability**

数据模型理解为可迭代的任何对象（它是本机数组，或者它具有可视化工具（NatVis 或其他）以使其可迭代）将具有一个迭代器函数（通过 ES6 标准符号进行索引）。 这意味着可以按如下方式在 JavaScript 中循环访问本机对象。

```javascript
function iterateNative(nativeObject)
{
    for (var val of nativeObject)
    {
        // 
        // val will contain each element iterated from the native object.  This would be each element of an array,
        // each element of an STL structure which is made iterable through NatVis, each element of a data structure
        // which has a JavaScript iterator accessible via [Symbol.iterator], or each element of something
        // which is made iterable via support of IIterableConcept in C/C++.
        //
    }
}
```

**可索引性**

通过序数（例如：本机数组）在一个维度中理解为可索引的对象可在 JavaScript 中通过标准属性访问运算符--对象\[索引\]进行索引编制。 如果按名称对对象进行索引或在多个维度中可编制索引，则会将 getValueAt 和 setValueAt 方法投影到对象，以便 JavaScript 代码可以利用索引器。

```javascript
function indexNative(nativeArray)
{
    var first = nativeArray[0];
}
```

**字符串转换**

通过支持 IStringDisplayableConcept 或 NatVis DisplayString 元素，具有显示字符串转换的任何本机对象都具有通过标准 JavaScript toString 方法访问的字符串转换。

```javascript
function stringifyNative(nativeObject)
{
    var myString = nativeObject.toString();
}
```

## <a name="span-idcreating_native_debugger_objectsspanspan-idcreating_native_debugger_objectsspanspan-idcreating_native_debugger_objectsspancreating-native-debugger-objects"></a><span id="Creating_Native_Debugger_Objects"></span><span id="creating_native_debugger_objects"></span><span id="CREATING_NATIVE_DEBUGGER_OBJECTS"></span>创建本机调试器对象

如前所述，JavaScript 脚本可以通过几种方式之一将其传递到 JavaScript 中来访问本机对象，也可以通过调用主机库来创建本机对象。 使用以下函数创建本机调试器对象。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">付款方式</th>
<th align="left">签名</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>getModuleSymbol</p></td>
<td align="left"><p>getModuleSymbol （moduleName，symbolName，[contextInheritor]）</p>
<p>getModuleSymbol （moduleName，symbolName，[typeName]，[contextInheritor]）</p></td>
<td align="left"><p>返回特定模块中全局符号的对象。 模块名称和符号名称是字符串。</p>
<p>如果提供了可选的<em>contextInheritor</em>参数，则会在与传递的对象相同的上下文（地址空间，调试目标）中查找模块和符号。 如果未提供参数，则会在调试器的当前上下文中查找模块和符号。 不是一次性测试脚本的 JavaScript 扩展应始终提供显式上下文。</p>
<p>如果提供了可选的<em>typeName</em>参数，则认为符号是传递的类型，并且将忽略符号中指示的类型。 请注意，任何需要在模块的公共符号上操作的调用方应始终提供显式类型名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>createPointerObject</p></td>
<td align="left"><p>createPointerObject （address，moduleName，typeName，[contextInheritor]）</p></td>
<td align="left"><p>在指定的地址或位置创建指针对象。 模块名称和类型名称为字符串。</p>
<p>如果提供了可选的<em>contextInheritor</em>参数，则会在与传递的对象相同的上下文（地址空间，调试目标）中查找模块和符号。 如果未提供参数，则会在调试器的当前上下文中查找模块和符号。 不是一次性测试脚本的 JavaScript 扩展应始终提供显式上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>createTypedObject</p></td>
<td align="left"><p>createTypedObject （location，moduleName，typeName，[contextInheritor]）</p></td>
<td align="left"><p>创建一个对象，该对象表示位于指定位置的调试目标的地址空间内的本机类型化对象。 模块名称和类型名称为字符串。</p>
<p>如果提供了可选的<em>contextInheritor</em>参数，则会在与传递的对象相同的上下文（地址空间，调试目标）中查找模块和符号。 如果未提供参数，则会在调试器的当前上下文中查找模块和符号。 不是一次性测试脚本的 JavaScript 扩展应始终提供显式上下文。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idhost-apisspanspan-idhost-apisspanspan-idhost-apisspanhost-apis-for-javascript-extensions"></a><span id="Host-APIs"></span><span id="host-apis"></span><span id="HOST-APIS"></span>JavaScript 扩展的宿主 Api


JavaScript 提供程序将一个名为 host 的对象插入到它加载的每个脚本的全局命名空间中。 此对象提供对脚本的关键功能的访问权限，并提供对调试器的命名空间的访问权限。 它分两个阶段进行设置。

-   **阶段 1**：在执行任何脚本之前，主机对象只包含脚本自行初始化并注册其扩展点（作为生成者和使用者）所需的最小功能集。 根代码和初始化代码不用于操作调试目标的状态或执行复杂的操作，因此，在 initializeScript 方法返回后，主机不会完全填充。

-   **阶段 2**：InitializeScript 返回后，将用操作调试目标状态所需的所有内容来填充主机对象。

**宿主对象级别**

部分关键功能直接位于主机对象下。 余数为带命名空间。 命名空间包括以下各项。

| 命名空间   | 描述                                                              |
|-------------|--------------------------------------------------------------------------|
| 功能 | 有助于诊断和调试脚本代码的功能    |
| memory      | 用于在调试目标内启用内存读写功能的功能 |

 

**根级别**

直接在宿主对象中，可以找到以下属性、方法和构造函数。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">路径名</th>
<th align="left">签名</th>
<th align="left">存在阶段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">createPointerObject</td>
<td align="left"><p>createPointerObject （address，moduleName，typeName，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">在指定的地址或位置创建指针对象。 模块名称和类型名称为字符串。 可选的<strong>contextInheritor</strong>参数与 getModuleSymbol 的工作方式相同。</td>
</tr>
<tr class="even">
<td align="left">createTypedObject</td>
<td align="left"><p>createTypedObject （location，moduleName，typeName，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">创建一个对象，该对象表示位于指定位置的调试目标的地址空间内的本机类型化对象。 模块名称和类型名称为字符串。 可选的 contextInheritor 参数与 getModuleSymbol 的工作方式相同。</td>
</tr>
<tr class="odd">
<td align="left">currentProcess</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">返回对象，该对象表示调试器的当前进程</td>
</tr>
<tr class="even">
<td align="left">currentSession</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">返回对象，该对象表示正在调试的调试器的当前会话（目标、转储等）</td>
</tr>
<tr class="odd">
<td align="left">Thread.currentthread.priority</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">返回表示调试器的当前线程的对象</td>
</tr>
<tr class="even">
<td align="left">evaluateExpression</td>
<td align="left"><p>evaluateExpression （expression，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">这会调用调试宿主，以仅使用调试目标的语言来计算表达式。 如果提供了可选的<em>contextInheritor</em>参数，则表达式将在参数的上下文（例如：地址空间和调试目标）中进行计算;否则，它将在调试器的当前上下文中进行计算</td>
</tr>
<tr class="odd">
<td align="left">evaluateExpressionInContext</td>
<td align="left"><p>evaluateExpressionInContext （context，expression）</p></td>
<td align="left">2</td>
<td align="left">这会调用调试宿主，以仅使用调试目标的语言来计算表达式。 上下文参数指示要用于计算的隐式此指针。 表达式将在<em>上下文参数指示的上下文（</em>例如：地址空间和调试目标）中进行计算。</td>
</tr>
<tr class="even">
<td align="left">getModuleSymbol</td>
<td align="left"><p>getModuleSymbol （moduleName，symbolName，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">返回特定模块中全局符号的对象。 模块名称和符号名称是字符串。 如果提供了可选的<em>contextInheritor</em>参数，则会在与传递的对象相同的上下文（地址空间，调试目标）中查找模块和符号。 如果未提供参数，则会在调试器的当前上下文中查找模块和符号。 不是一次性脚本的 JavaScript 扩展应始终提供显式上下文</td>
</tr>
<tr class="odd">
<td align="left">getNamedModel</td>
<td align="left"><p>getNamedModel （modelName）</p></td>
<td align="left">2</td>
<td align="left">返回针对给定名称注册的数据模型。 请注意，针对尚未注册的名称调用此方法是完全合法的。 这样做将为该名称创建一个存根，并在注册时对实际对象执行存根的操作</td>
</tr>
<tr class="even">
<td align="left">indexedValue</td>
<td align="left"><p>new indexedValue （value，索引）</p></td>
<td align="left">2</td>
<td align="left">对象的构造函数，可从 JavaScript 迭代器返回该构造函数，以便将默认的索引集分配给迭代值。 索引集必须表示为 JavaScript 数组。</td>
</tr>
<tr class="odd">
<td align="left">Int64</td>
<td align="left"><p>新 Int64 （value，[highValue]）</p></td>
<td align="left">1</td>
<td align="left">这将构造一个库 Int64 类型。 单个参数版本将采用任何可打包为 Int64 的值（不转换）并将其放入其中。 如果提供了可选的第二个参数，则第一个参数的转换将打包到较低的32位，并将第二个参数的转换打包到高位32位。</td>
</tr>
<tr class="even">
<td align="left">namedModelParent</td>
<td align="left"><p>new namedModelParent （object，name）</p></td>
<td align="left">1</td>
<td align="left">要放置在从<strong>initializeScript</strong>返回的数组中的对象的构造函数，这表示使用 JavaScript 原型或 ES6 类作为具有给定名称的数据模型的数据模型父扩展</td>
</tr>
<tr class="odd">
<td align="left">namedModelRegistration</td>
<td align="left"><p>new namedModelRegistration （object，name）</p></td>
<td align="left">1</td>
<td align="left">要放置在从<strong>initializeScript</strong>返回的数组中的对象的构造函数，这表示通过已知名称将 JavaScript 原型或 ES6 类注册为数据模型，以便其他扩展可以查找和扩展</td>
</tr>
<tr class="even">
<td align="left">命名空间</td>
<td align="left"><p>属性</p></td>
<td align="left">2</td>
<td align="left">提供对调试器的根命名空间的直接访问。 例如，可以通过主机访问第一个调试目标的进程列表。第一个（）。使用此属性的进程</td>
</tr>
<tr class="odd">
<td align="left">registerNamedModel</td>
<td align="left"><p>registerNamedModel （object，modelName）</p></td>
<td align="left">2</td>
<td align="left">这会将 JavaScript 原型或 ES6 类注册为具有给定名称的数据模型。 通过此类注册，可以通过其他脚本或其他调试器扩展来定位和扩展原型或类。 请注意，脚本应首选从其<strong>initializeScript</strong>方法返回<strong>namedModelRegistration</strong>对象，而不是强制执行此操作。 任何导致强制更改的脚本都需要具有<strong>initializeScript</strong>方法才能进行清理。</td>
</tr>
<tr class="even">
<td align="left">registerExtensionForTypeSignature</td>
<td align="left"><p>registerExtensionForTypeSignature （object，typeSignature）</p></td>
<td align="left">2</td>
<td align="left">这会将 JavaScript 原型或 ES6 类注册为提供的类型签名所给定的本机类型的扩展数据模型。 请注意，脚本应首选从其<strong>initializeScript</strong>方法返回<strong>typeSignatureExtension</strong>对象，而不是强制执行此操作。 任何导致强制更改的脚本都需要具有<strong>initializeScript</strong>方法才能进行清理。</td>
</tr>
<tr class="odd">
<td align="left">registerPrototypeForTypeSignature</td>
<td align="left"><p>registerPrototypeForTypeSignature （object，typeSignature）</p></td>
<td align="left">2</td>
<td align="left">对于提供的类型签名所给定的本机类型，此方法将 JavaScript 原型或 ES6 类注册为规范数据模型（例如：可视化工具）。 请注意，脚本应首选从其<strong>initializeScript</strong>方法返回<strong>typeSignatureExtension</strong>对象，而不是强制执行此操作。 任何导致强制更改的脚本都需要具有<strong>uninitializeScript</strong>方法才能进行清理。</td>
</tr>
<tr class="even">
<td align="left">Languageprimitives.parseint64</td>
<td align="left"><p>Languageprimitives.parseint64 （string，[基数]）</p></td>
<td align="left">1</td>
<td align="left">此方法的行为类似于标准 JavaScript parseInt 方法，不同之处在于它将改为返回库 Int64 类型。 如果提供了基数，则分析将以2、8、10或16的形式出现，如所示。</td>
</tr>
<tr class="odd">
<td align="left">typeSignatureExtension</td>
<td align="left"><p>new typeSignatureExtension （object，typeSignature，[moduleName]，[minVersion]，[maxVersion]）</p></td>
<td align="left">1</td>
<td align="left">要放置在从<strong>initializeScript</strong>返回的数组中的对象的构造函数，这表示通过 JavaScript 原型或 ES6 类通过类型签名描述的本机类型的扩展。 此类注册将 "添加字段" 添加到与签名匹配的任何类型的调试器可视化，而不是完全提取。 可选的模块名称和版本可以限制注册。 版本被指定为 "1.2.3.4" 样式字符串。</td>
</tr>
<tr class="even">
<td align="left">typeSignatureRegistration</td>
<td align="left"><p>new typeSignatureRegistration （object，typeSignature，[moduleName]，[minVersion]，[maxVersion]）</p></td>
<td align="left">1</td>
<td align="left">要放置在从<strong>initializeScript</strong>返回的数组中的对象的构造函数，这表示针对本机类型签名的 JavaScript 原型或 ES6 类的规范注册。 此类注册 "接管" 调试器与签名匹配的任何类型的可视化效果，而不只是扩展它。 可选的模块名称和版本可以限制注册。 版本被指定为 "1.2.3.4" 样式字符串。</td>
</tr>
<tr class="odd">
<td align="left">unregisterNamedModel</td>
<td align="left"><p>unregisterNamedModel （modelName）</p></td>
<td align="left">2</td>
<td align="left">这将从查找中取消注册数据模型，以撤消由<strong>registerNamedModel</strong>执行的任何操作</td>
</tr>
<tr class="even">
<td align="left">unregisterExtensionForTypeSignature</td>
<td align="left"><p>unregisterExtensionForTypeSignature （object，typeSignature，[moduleName]，[minVersion]，[maxVersion]）</p></td>
<td align="left">2</td>
<td align="left">这将从所提供的类型签名所给定的本机类型的扩展数据模型中注销 JavaScript 原型或 ES6 类。 这是 registerExtensionForTypeSignature 的逻辑撤消。 请注意，脚本应首选从其<strong>initializeScript</strong>方法返回<strong>typeSignatureExtension</strong>对象，而不是强制执行此操作。 任何导致强制更改的脚本都需要具有<strong>initializeScript</strong>方法才能进行清理。 可选的模块名称和版本可以限制注册。 版本被指定为 "1.2.3.4" 样式字符串。</td>
</tr>
<tr class="odd">
<td align="left">unregisterPrototypeForTypeSignature</td>
<td align="left"><p>unregisterPrototypeForTypeSignature （object，typeSignature，[moduleName]，[minVersion]，[maxVersion]）</p></td>
<td align="left">2</td>
<td align="left">这将从提供的类型签名所给定的本机类型中注销 JavaScript 原型或 ES6 类（例如：可视化工具）。 这是 registerPrototypeForTypeSignature 的逻辑撤消。 请注意，脚本应首选从其<strong>initializeScript</strong>方法返回<strong>typeSignatureRegistration</strong>对象，而不是强制执行此操作。 任何导致强制更改的脚本都需要具有<strong>uninitializeScript</strong>方法才能进行清理。 可选的模块名称和版本可以限制注册。 版本被指定为 "1.2.3.4" 样式字符串。</td>
</tr>
</tbody>
</table>

**诊断功能**

宿主对象的诊断子命名空间包含以下各项。

| 名称     | 签名           | 存在阶段 | 描述                                                                                                                                                                                                                                                                                                                                                   |
|----------|---------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| debugLog | debugLog （对象 ...） | 1             | 这为脚本扩展提供了 printf 样式的调试。 目前，debugLog 的输出将路由到调试器的输出控制台。 在以后的某个时间点，还提供了一些计划以灵活地路由此输出。 注意：不应将其用作将用户输出打印到控制台的方法。 将来可能不会将其路由。 |

 

**内存功能**

宿主对象的内存子命名空间包含以下各项。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">路径名</th>
<th align="left">签名</th>
<th align="left">存在阶段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">readMemoryValues</td>
<td align="left"><p>readMemoryValues （location，numElements，[elementSize]，[isSigned]，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">这会从调试目标的地址空间读取值的原始数组，并将类型化数组放在此内存视图的顶部。 提供的位置可以是地址（64位值）、位置对象或本机指针。 数组的大小由<em>numElements</em>参数指示。 数组中每个元素的大小（和类型）由可选的<em>elementSize</em>和<em>isSigned</em>参数提供。 如果未提供此类参数，则默认值为 byte （无符号/1 字节）。 如果提供了可选的<em>contextInheritor</em>参数，则将在参数指示的上下文中读取内存（例如：地址空间和调试目标）;否则，将从调试器的当前上下文中读取它。 请注意，在8、16和32位值上使用此方法会导致在读取内存上放置快速类型化的视图。 在64位值上使用此方法会导致构建64位库类型的数组，这会大大增加成本。</td>
</tr>
<tr class="even">
<td align="left">readString</td>
<td align="left"><p>readString （location，[contextInheritor]）</p>
<p>readString （location，[length]，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">这会从调试目标的地址空间读取一个窄（当前代码页）字符串，将其转换为 UTF-16，并将结果作为 JavaScript 字符串返回。 如果无法读取内存，则可能会引发异常。 提供的位置可以是地址（64位值）、位置对象或本机 char<em>。 如果提供了可选的<em>contextInheritor</em>参数，则将在参数指示的上下文中读取内存（例如：地址空间和调试目标）;否则，将从调试器的当前上下文中读取它。 如果提供了可选<em>长度</em>参数，则读取字符串将为指定长度。</td>
</tr>
<tr class="odd">
<td align="left">readWideString</td>
<td align="left"><p>readWideString （location，[contextInheritor]）</p>
<p>readWideString （location，[length]，[contextInheritor]）</p></td>
<td align="left">2</td>
<td align="left">这会从调试目标的地址空间读取宽（UTF-16）字符串，并将结果作为 JavaScript 字符串返回。 如果无法读取内存，则可能会引发异常。 提供的位置可以是地址（64位值）、位置对象或本机 wchar_t</em>。 如果提供了可选的<em>contextInheritor</em>参数，则将在参数指示的上下文中读取内存（例如：地址空间和调试目标）;否则，将从调试器的当前上下文中读取它。 如果提供了可选<em>长度</em>参数，则读取字符串将为指定长度。</td>
</tr>
</tbody>
</table>

 

## <a name="span-iddata-modelspanspan-iddata-modelspanspan-iddata-modelspandata-model-concepts-in-javascript"></a><span id="Data-Model"></span><span id="data-model"></span><span id="DATA-MODEL"></span>JavaScript 中的数据模型概念


**数据模型映射**

以下数据模型概念映射到 JavaScript。

| 概念                 | 本机接口             | JavaScript 等效项                                                |
|-------------------------|------------------------------|----------------------------------------------------------------------|
| 字符串转换       | IStringDisplayableConcept    | standard： toString （...）{...}                                         |
| Iterability             | IIterableConcept             | 标准\[Symbol. iterator\]（） {...}                                 |
| 可索引性            | IIndexableConcept            | protocol： getDimensionality （...）/getValueAt （...）/setValueAt （...） |
| 运行时类型转换 | IPreferredRuntimeTypeConcept | protocol： getPreferredRuntimeTypedObject （...）                        |

 

**字符串转换**

字符串转换概念（IStringDisplayableConcept）直接转换为标准 JavaScript **toString**方法。 由于所有 JavaScript 对象都具有字符串转换（如果未在其他位置提供，否则由对象原型提供），返回到数据模型的每个 JavaScript 对象都可以转换为显示字符串。 重写字符串转换只需实现自己的 toString。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IStringDisplayableConcept::ToDisplayString(...)
    //
    toString()
    { 
        return "This is my own string conversion!";
    }
}
```

**Iterability**

数据模型的概念：对象是可迭代还是不映射到对象是否为可迭代的 ES6 协议。 具有\[符号的任何对象。 iterator\]方法被视为可迭代。 此类的实现将使对象可迭代。

仅可迭代的对象可以具有如下实现。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        yield "First Value";
        yield "Second Value";
        yield "Third Value";
    }
}
```

必须特别注意的是可迭代和可编制索引的对象，因为从迭代器返回的对象必须通过特殊返回类型包括索引和值。

**可迭代和可编制索引**

可迭代和可编制索引的对象需要迭代器中有一个特殊的返回值。 迭代器生成 indexedValue 的实例，而不是生成值。 将索引作为 indexedValue 构造函数的第二个参数中的数组进行传递。 它们可以是多维的，但必须与索引器协议中返回的维数匹配。

此代码显示了一个示例实现。

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIterableConcept::GetIterator
    //
    *[Symbol.iterator]()
    {
        //
        // Consider this a map which mapped 42->"First Value", 99->"Second Value", and 107->"Third Value"
        //
        yield new host.indexedValue("First Value", [42]);
        yield new host.indexedValue("Second Value", [99]);
        yield new host.indexedValue("Third Value", [107]);
    }
}
```

**可索引性**

与 JavaScript 不同，数据模型在属性访问和索引编制之间做出非常明显的区别。 希望在数据模型中表现为可编制索引的任何 JavaScript 对象必须实现一个协议，该协议包含 getDimensionality 方法，该方法返回索引器的维数和可选的 getValueAt 和 setValueAt 方法对。在提供的索引执行对象的读取和写入。 如果对象为只读或只写，则可接受省略 getValueAt 或 setValueAt 方法

```javascript
class myObject
{
    //
    // This method will be called whenever any native code calls IIndexableConcept::GetDimensionality or IIterableConcept::GetDefaultIndexDimensionality
    //
    getDimensionality()
    {
        //
        // Pretend we are a two dimensional array.
        //
        return 2;
    } 

    //
    // This method will be called whenever any native code calls IIndexableConcept::GetAt
    //
    getValueAt(row, column)
    {
        return this.__values[row * this.__columnCount + column];
    }

    //
    // This method will be called whenever any native code calls IIndexableConcept::SetAt
    //
    setValueAt(value, row, column)
    {
        this.__values[row * this.__columnCount + column] = value;
    }
}
```

**运行时类型转换**

这仅适用于针对类型系统（本机）类型注册的 JavaScript 原型/类。 调试器通常能够执行分析（例如，运行时类型信息（RTTI）/v-表分析），以从用代码表示的静态类型确定对象的真实运行时类型。 针对本机类型注册的数据模型可以通过 IPreferredRuntimeTypeConcept 的实现来重写此行为。 同样，针对本机对象注册的 JavaScript 类或原型可以通过实现由 getPreferredRuntimeTypedObject 方法组成的协议来提供自己的实现。

请注意，虽然此方法在技术上可以返回任何内容，但它会被视为错误的窗体，以便它返回的内容并不是真正的运行时类型或派生类型。 这种情况可能会使调试器的用户产生严重的混淆。 但是，重写此方法可以对 C 样式标头和实现的对象样式等对象（例如）进行比较。

```javascript
class myNativeModel
{
    //
    // This method will be called whenever the data model calls IPreferredRuntimeTypeConcept::CastToPreferredRuntimeType
    //
    getPreferredRuntimeTypedObject()
    {
        var loc = this.targetLocation;

        //
        // Perform analysis...
        //
        var runtimeLoc = loc.Add(runtimeObjectOffset);
  
        return host.createTypedObject(runtimeLoc, runtimeModule, runtimeTypeName);
    }
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)

[JavaScript 扩展中的本机调试器对象-设计和测试注意事项](native-objects-in-javascript-extensions-design-considerations.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)