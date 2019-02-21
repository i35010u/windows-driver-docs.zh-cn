---
title: 调试器数据模型 c + + 对象
description: 本主题介绍如何使用调试器数据模型 c + + 对象以及它们如何扩展调试器的功能。
ms.date: 10/08/2018
ms.openlocfilehash: df747dd779761f71a07ec23085f991287c36f518
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542455"
---
# <a name="debugger-data-model-c-objects"></a>调试器数据模型 c + + 对象

本主题介绍如何使用调试器数据模型 c + + 对象以及它们如何扩展调试器的功能。

本主题是一系列用于描述可从 c + +、 如何使用它们来构建基于 c + + 调试器扩展，以及如何使访问接口的一部分使用的数据模型的其他构造 (例如：JavaScript 或 NatVis） 从 c + + 数据模型扩展插件。


[调试程序数据模型 c + + 概述](data-model-cpp-overview.md)

[调试器数据模型 c + + 接口](data-model-cpp-interfaces.md)

[调试器数据模型 c + + 对象](data-model-cpp-objects.md)

[调试器数据模型 c + + 其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 c + + 概念](data-model-cpp-concepts.md)

[C + + 编写脚本的调试程序数据模型](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>主题部分

本主题包含以下部分：

[核心调试器对象模型](#core)

[调试器数据模型核心对象类型](#objecttypes)

[调试器数据模型管理器](#modelmanager)

---

## <a name="span-idcore--the-core-debugger-object-model"></a><span id="core">  核心调试器对象模型

有关数据模型的最基本但功能强大的项目之一是它标准化的哪些对象是一个与对象交互的方式定义。 *IModelObject*接口封装的对象-概念，无论该对象是一个整数、 浮点值、 字符串、 调试器的目标地址空间中一些复杂类型还是一些调试程序的概念等进程或模块的概念。

有几种不同方法可保存在 （或装箱到） *IModelObject*:

-   **内部值**-一个*IModelObject*可以是多个基本类型的容器：8、 16、 32 或 64 位有符号或无符号整数、 布尔值、 字符串、 错误或为空这一概念。

-   **本机对象**-一个*IModelObject*可以表示复杂类型 （如调试器的类型系统所定义） 内的任何目标调试器的地址空间 
    
-   **综合对象**-一个*IModelObject*如果您愿意，可以是动态对象-字典： 一系列键 / 值 / 元数据元组和一组**概念**用于定义应用行为的不只是表示键 / 值对。

-   **属性**-一个*IModelObject*可以表示一个属性： 可检索其值，或将其更改与方法调用的内容。 中的属性*IModelObject*实际上是*IModelPropertyAccessor*接口装箱到*IModelObject*

-   **方法**-一个*IModelObject*可以表示一种方法： 内容您可以使用一组参数调用并获取返回值。 中的一个方法*IModelObject*实际上是*IModelMethod*接口装箱到*IModelObject*

### <a name="extensibility-within-the-object-model"></a>对象模型中的可扩展性

*IModelObject*不是单独的对象。 除了表示上面所示的对象的类型之一，每个对象具有父数据模型的链的这一概念。 此证书链的行为非常类似于[JavaScript 原型链](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)。
而不是原型的线性链具有 JavaScript，正如每个数据模型对象定义的线性链**的父模型**。 每个这些父模型又有自己的父项集的另一个线性链。 从本质上讲，每个对象本身和此树中的每个对象的是功能 （属性、 等） 的聚合。 查询的特定属性时，如果在查询的对象不支持该属性，查询是按线性顺序传递到每个父反过来。 这将创建的聚合树的深度优先搜索位置解析为属性搜索的行为。

此对象模型中的可扩展性是非常简单提供其自身的聚合和父模型的树，是每个对象这一概念。 扩展可以进入并将其自身添加到列表中的另一个对象的父模型。 执行此操作**扩展了**对象。 在这种方式，很可能要添加到任何内容的功能： 对象或值、 本机类型、 调试器的概念的哪个进程或线程的特定实例，或甚至是"所有可迭代对象"这一概念。

### <a name="context-context-and-context-the-this-pointer-the-address-space-and-implementation-private-data"></a>上下文、 上下文和上下文：**这**指针、 地址空间和实现专用数据

有三个的概念**上下文**就必须了解对象模型的上下文中执行。

#### <a name="context-the-this-pointer"></a>上下文：**这**指针

由于可能会在数据模型树的任何级别实现给定的属性或方法，因此它是所需的方法或属性，以便能够访问原始对象的实现 (所谓**这**c + + 中的指针或**这**在 JavaScript 中的对象。 该实例对象传递到各种方法的第一个参数调用**上下文**中所述的方法。

#### <a name="context-the-address-space"></a>上下文：地址空间

请务必注意，与以前的扩展不同模型的位置**上下文**（目标、 进程、 线程正在查看） 是相对于当前用户界面状态时，数据模型接口通常采用此上下文中的所有 Api 的 UI 概念显式或隐式作为*IDebugHostContext*接口。 每个*IModelObject*模型数据中包含此类型的上下文信息，以及它和可以传播到对象，它将返回该上下文。 这意味着，当读取本机值或扩展的一个关键价值*IModelObject*，它将读取超出目标和其中对象已从最初获取的过程。

没有显式的常量值，**使用\_当前\_主机\_上下文**，，可以传递给方法采用*IDebugHostContext*参数。 此值指示上下文应确实是调试器的当前 UI 状态。 这一概念，但是，需要为显式。

#### <a name="context-implementation-private-data"></a>上下文：实现私有数据

请记住，每个对象的数据模型中实际对象实例的聚合和附加的父模型的树。
每个这些父模型 （这可以在许多不同的对象的链链接） 可以将私有实现数据与任何实例对象相关联。 每个*IModelObject*它在概念上创建具有特定的父模型映射到定义的私有实例数据的哈希表*IUnknown*接口。 这允许一个父模型来缓存每个实例上的信息或否则具有任意相关联的数据。

通过访问此类型的上下文*GetContextForDataModel*并*SetContextForDataModel*上的方法*IModelObject*。




## <a name="span-idimodelobjectspan-the-core-debugger-object-interface-imodelobject"></a><span id="imodelobject"></span> 核心调试器对象接口：**IModelObject**

-------------------------------------------

*IModelObject*接口定义，如下所示：

```cpp
DECLARE_INTERFACE_(IModelObject, IUnknown)
{
    STDMETHOD(QueryInterface)(_In_ REFIID iid, _COM_Outptr_ PVOID* iface);
    STDMETHOD_(ULONG, AddRef)();
    STDMETHOD_(ULONG, Release)() PURE;
    STDMETHOD(GetContext)(_COM_Outptr_result_maybenull_ IDebugHostContext** context) PURE;
    STDMETHOD(GetKind)(_Out_ ModelObjectKind *kind) PURE;
    STDMETHOD(GetIntrinsicValue)(_Out_ VARIANT* intrinsicData);
    STDMETHOD(GetIntrinsicValueAs)(_In_ VARTYPE vt, _Out_ VARIANT* intrinsicData) PURE;
    STDMETHOD(GetKeyValue)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetKeyValue)(_In_ PCWSTR key, _In_opt_ IModelObject* object) PURE;
    STDMETHOD(EnumerateKeyValues)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
    STDMETHOD(GetRawValue)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(EnumerateRawValues)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
    STDMETHOD(Dereference)(_COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(TryCastToRuntimeType)(_COM_Errorptr_ IModelObject** runtimeTypedObject) PURE;
    STDMETHOD(GetConcept)(_In_ REFIID conceptId, _COM_Outptr_ IUnknown** conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore** conceptMetadata) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetTypeInfo)(_Out_ IDebugHostType** type) PURE;
    STDMETHOD(GetTargetInfo)(_Out_ Location* location, _Out_ IDebugHostType** type) PURE;
    STDMETHOD(GetNumberOfParentModels)(_Out_ ULONG64* numModels) PURE;
    STDMETHOD(GetParentModel)(_In_ ULONG64 i, _COM_Outptr_ IModelObject **model, _COM_Outptr_result_maybenull_ IModelObject **contextObject) PURE;
    STDMETHOD(AddParentModel)(_In_ IModelObject* model, _In_opt_ IModelObject* contextObject, _In_ bool override) PURE;
    STDMETHOD(RemoveParentModel)(_In_ IModelObject* model) PURE;
    STDMETHOD(GetKey)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(GetKeyReference)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** objectReference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetKey)(_In_ PCWSTR key, _In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
    STDMETHOD(ClearKeys)() PURE;
    STDMETHOD(EnumerateKeys)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
    STDMETHOD(EnumerateKeyReferences)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
    STDMETHOD(SetConcept)(_In_ REFIID conceptId, _In_ IUnknown* conceptInterface, _In_opt_ IKeyStore* conceptMetadata) PURE;
    STDMETHOD(ClearConcepts)() PURE;
    STDMETHOD(GetRawReference)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(EnumerateRawReferences)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
    STDMETHOD(SetContextForDataModel)(_In_ IModelObject* dataModelObject, _In_ IUnknown* context) PURE;
    STDMETHOD(GetContextForDataModel)(_In_ IModelObject* dataModelObject, _Out_ IUnknown** context) PURE;
    STDMETHOD(Compare)(_In_ IModelObject* other, _COM_Outptr_opt_result_maybenull_ IModelObject **ppResult) PURE;
    STDMETHOD(IsEqualTo)(_In_ IModelObject* other, _Out_ bool* equal) PURE;
}
```

**基本方法**

以下是对象的适用于任何类型由 IModelObject 的常规方法。 

```cpp
STDMETHOD(GetKind)(_Out_ ModelObjectKind *kind) PURE;
STDMETHOD(GetContext)(_COM_Outptr_result_maybenull_ IDebugHostContext** context) PURE;
STDMETHOD(GetIntrinsicValue)(_Out_ VARIANT* intrinsicData);
STDMETHOD(GetIntrinsicValueAs)(_In_ VARTYPE vt, _Out_ VARIANT* intrinsicData) PURE;
STDMETHOD(Compare)(_In_ IModelObject* other, _COM_Outptr_opt_result_maybenull_ IModelObject **ppResult) PURE;
STDMETHOD(IsEqualTo)(_In_ IModelObject* other, _Out_ bool* equal) PURE;
STDMETHOD(Dereference)(_COM_Errorptr_ IModelObject** object) PURE;
```

[GetKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkind) 

GetKind 方法返回的对象类型的装箱 IModelObject 内。 

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getcontext)

GetContext 方法返回与对象相关联的主机上下文。 

[GetIntrinsicValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getintrinsicvalue)

GetIntrinsicValue 方法将返回其装箱 IModelObject 内的一件事。 表示一个装箱 IModelObject 接口上只有合法调用此方法内部函数或一个特定接口，进行装箱。 它不能在本机对象，没有值的对象，综合对象上调用，并且引用的对象。 GetIntrinsicValueAs 方法的行为非常类似于 GetIntrinsicValue 方法，只不过它将值转换为指定的变量类型。 如果不能执行转换，该方法将返回错误。

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-isequalto)

IsEqualTo 方法比较两个模型对象，并返回它们是否相等值中。 对于已排序的对象，此方法返回 true 等同于比较方法返回 0。 有没有一定的顺序，但都是可以相等的对象，该比较方法将失败，但这将不会。 由对象的类型定义的基于值比较意义。 目前，这是仅为内部类型和定义错误对象。 Equatability 没有当前数据模型概念。 

[取消引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-dereference)

取消引用方法取消引用一个对象。 此方法可用于取消引用的数据模型基于引用 （ObjectTargetObjectReference，ObjectKeyReference） 或本机语言引用 （指针或语言参考）。 请务必注意，此方法将删除对对象的引用语义的单个级别。 它是完全可以，例如，具有对语言引用的数据模型引用。 在这种情况下，第一次调用取消引用方法会删除数据模型参考和保留的语言参考。 在得到的对象上调用取消引用将随后删除的语言参考，并且返回下该引用的本机值。 


**密钥操作方法**

这是字典键、 值和元数据元组的任何综合对象具有一系列的方法处理这些密钥和值，并与之关联的元数据。 

基于值形式的 Api 都是： 

```cpp
STDMETHOD(GetKeyValue)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(SetKeyValue)(_In_ PCWSTR key, _In_opt_ IModelObject* object) PURE;
STDMETHOD(EnumerateKeyValues)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
The key based forms of the APIs (including those used for key creation) are: 
STDMETHOD(GetKey)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(SetKey)(_In_ PCWSTR key, _In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
STDMETHOD(EnumerateKeys)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
STDMETHOD(ClearKeys)() PURE;
```

引用基于窗体的 api 是： 

```cpp
STDMETHOD(GetKeyReference)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** objectReference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(EnumerateKeyReferences)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
```

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkeyvalue)

GetKeyValue 方法是第一种方法以获取的值 （和关联的元数据），客户端将转换为给定的键的名称。 如果键是属性访问器-的是它的值即是装箱的 IModelPropertyAccessor IModelObject，GetKeyValue 方法将自动调用以检索实际值属性访问器的 GetValue 方法。

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setkeyvalue)

SetKeyValue 方法是客户端将以设置密钥的值转换为第一种方法。 此方法不能用于为对象创建新的密钥。 它仅将设置现有键的值。 请注意几个密钥都是只读的 (例如： 属性访问器可从 SetValue 方法返回 E_NOT_IMPL 实现)。 在调用时读取仅密钥，此方法将失败。 

[EnumerateKeyValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyvalues)

EnumerateKeyValues 方法是客户端会变为以枚举所有 （这包括在父模型的树中任何位置实现的所有键） 的对象上的键的第一个方法。 务必要注意 EnumerateKeyValues 将枚举定义重复的名称，在对象树中的任何密钥但是-GetKeyValue 和 SetKeyValue 等方法将仅处理具有给定名称的键的第一个实例，发现的深度优先遍历。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkey)

GetKey 方法将获取的值 （和使用关联的元数据） 的给定的键的名称。 大多数客户端应改为使用 GetKeyValue 方法。 如果对密钥进行属性访问器，调用此方法将返回到 IModelObject 装箱属性访问器 （IModelPropertyAccessor 接口）。 与不同 GetKeyValue，此方法不会自动解决的基础值的密钥通过调用 GetValue 方法。 该职责是调用方的。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setkey)

Setkey 权限方法是客户端的方法将转换为以在对象上创建一个密钥 （和可能会将元数据与创建的密钥相关联）。 如果给定的对象已有具有给定名称的密钥，将出现两个问题之一。 如果密钥是在此给定的实例，因为如果不存在原始密钥将替换该注册表项的值。 如果手动，键是给定此实例的父数据模型的链中，将提供此实例上创建具有给定名称的新密钥。 这将实际上，导致对象具有相同的名称 （类似于派生类隐藏具有相同名称作为基类的成员） 的两个密钥。 

[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeys)

EnumerateKeys 方法的行为类似于 EnumerateKeyValues 方法，只不过它不会自动解析对象上的属性访问器。 这意味着如果键的值属性访问器，EnumerateKeys 方法将返回的属性访问器 (IModelPropertyAccessorInterface) 到 IModelObject 装箱，而不是自动调用 GetValue 方法。 这是类似于 GetKey 和 GetKeyValue 之间的差异。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-clearkeys)

ClearKeys 方法从指定的对象的实例中删除所有键及其关联的值和元数据。 此方法不起父模型附加到特定对象实例上。 

[GetKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkeyreference)

GetKeyReference 方法将搜索对象 （或其父模型链） 上的给定名称的密钥，并返回对该注册表项提供由装箱到 IModelObject IModelKeyReference 接口的引用。 该引用随后可用于获取或设置键的值。 

[EnumerateKeyReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyreferences)

EnumerateKeyReferences 方法的行为类似于 EnumerateKeyValues 方法，只不过它而不是键的值返回它枚举 （如果有由装箱到 IModelObject IModelKeyReference 接口） 的密钥对的引用。 可以使用此类引用要获取或设置密钥的基础值。 


**概念操作方法**

除了在元数据键/值元组的字典的模型对象，它也是容器的概念。 一个概念是抽象的或由对象可以执行。 从本质上讲，概念是一个动态对象支持的接口的存储。 立即由数据模型定义多个概念： 

概念接口 | 描述
------------------|-------------
IDataModelConcept | 这一概念是一个父模型。 如果此模型会自动附加到通过已注册的类型签名的本机类型，InitializeObject 方法将自动调用每次实例化此类类型的新对象。
IStringDisplayableConcept  | 对象可以转换为用于显示目的的字符串。
IIterableConcept  | 对象是一个容器，并且可以循环访问。
IIndexableConcept  | 该对象是一个容器，并且可以进行索引 （通过随机访问访问） 中一个或多个维度。
IPreferredRuntimeTypeConcept  | 该对象了解有关派生自它不是基础类型系统能够提供，并且想要处理其自身从静态到运行时类型的转换的类型的详细信息。
IDynamicKeyProviderConcept | 对象是动态的提供程序的密钥，并且想要接管的核心数据模型中的所有键查询。 此接口通常用作与 JavaScript 等动态语言的桥梁。
IDynamicConceptProviderConcept  | 对象是动态的提供程序的概念，并且想要接管的核心数据模型中的所有概念查询。 此接口通常用作与 JavaScript 等动态语言的桥梁。

IModelObject 上的以下方法用来操作对象支持的概念。 

```cpp
STDMETHOD(GetConcept)(_In_ REFIID conceptId, _COM_Outptr_ IUnknown** conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore** conceptMetadata) PURE;
STDMETHOD(SetConcept)(_In_ REFIID conceptId, _In_ IUnknown* conceptInterface, _In_opt_ IKeyStore* conceptMetadata) PURE;
STDMETHOD(ClearConcepts)() PURE;
```

[GetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getconcept)

GetConcept 方法将搜索对对象 （或其父模型链） 的概念，并返回到概念接口的接口指针。 行为和概念接口上的方法是特定于每个概念。 务必要注意，许多概念接口要求调用方将上下文对象显式传递 (或其中一个可能通常称之为此指针)。 请务必确保将正确的上下文对象传递给每个概念的接口。

[SetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setconcept)

SetConcept 方法会将此指定的对象实例上的指定的概念指针。 如果附加到此指定的对象实例的父模型还支持这一概念，该实例中的实现将覆盖的父模型中。 

[ClearConcepts](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-clearconcepts)

ClearConcepts 方法将从指定的对象的实例中删除所有概念。 


**本机对象方法**

虽然很多个模型对象引用的内部函数 (例如： 整数、 字符串) 或综合构造 （元数据键/值元组和概念的字典），模型对象还可以参阅本机构造 (例如： 调试的地址空间中的用户定义类型目标）。 IModelObject 接口具有一系列的方法对其进行访问此类本机对象的信息。 这些方法包括： 

```cpp
STDMETHOD(GetRawValue)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(EnumerateRawValues)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
STDMETHOD(TryCastToRuntimeType)(_COM_Errorptr_ IModelObject** runtimeTypedObject) PURE;
STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
STDMETHOD(GetTypeInfo)(_Out_ IDebugHostType** type) PURE;
STDMETHOD(GetTargetInfo)(_Out_ Location* location, _Out_ IDebugHostType** type) PURE;
STDMETHOD(GetRawReference)(_In_ SymbolKind kind, _In_ PCWSTR name, _In_ ULONG searchFlags, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(EnumerateRawReferences)(_In_ SymbolKind kind, _In_ ULONG searchFlags, _COM_Outptr_ IRawEnumerator** enumerator) PURE;
```

[GetRawValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getrawvalue)

GetRawValue 方法查找给定的对象中的本机构造。 此类构造可能是字段、 基本类、 字段中的基类、 成员函数，等等... 

[EnumerateRawValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawvalues)

EnumerateRawValues 方法枚举所有本机子项 (例如： 字段、 基类、 等) 的给定对象。 


[TryCastToRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-trycasttoruntimetype)

TryCastToRuntimeType 方法会询问调试主机来执行分析并确定实际运行时类型 (例如： 最派生的类) 的给定对象。 使用过度的精确分析特定于调试主机，可能包括 RTTI （c + + 运行时类型信息），检查的对象，或任何其他 V Table(virtual function table) 结构意味着，宿主可用于可靠地确定动态/运行时键入从静态类型。 无法转换为运行时类型并不意味着此方法调用将失败。 在这种情况下，该方法将返回给定的对象 (此指针) 的输出参数中。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getlocation) 

GetLocation 方法将返回的本机对象的位置。 虽然此类位置通常是调试目标的地址空间中的虚拟地址，但并不一定是这样。 此方法返回的位置是抽象的位置，可能是一个虚拟地址，可能指示在注册或子寄存器中的位置，或者可能表示某些其他任意地址空间定义的调试主机。 如果生成的位置对象的 HostDefined 字段为 0，它指示的位置是实际的虚拟地址。 可以通过检查生成的位置的偏移量字段检索此类虚拟地址。 HostDefined 字段的任何非零值指示偏移量字段的地址空间内的偏移量的备选电子邮件地址空间。 非零 HostDefined 值的确切含义是专用于调试主机。 

[GetTypeInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-gettypeinfo)

GetTypeInfo 方法将返回给定对象的本机类型。 如果对象不具有与之关联的本机类型信息 (例如： 它是内部函数，等...)，调用仍将成功，但将返回 null。 

[GetTargetInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-gettargetinfo)

GetTargetInfo 方法实际上是对象的 GetLocation 和 GetTypeInfo 方法返回同时抽象的位置，以及给定的本机类型的组合。 

[GetRawReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getrawreference)

GetRawReference 方法查找给定的对象中的本机构造并返回对它的引用。 此类构造可能是字段、 基本类、 字段中的基类、 成员函数，等等...务必要区分语言引用中返回此处 （ObjectTargetObjectReference 类型的对象） 的引用 (例如： c + + （& a) 或 & & 样式引用)。 

[EnumerateRawReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawreferences)

EnumerateRawReferences 方法枚举了对所有本机子级的引用 (例如： 字段、 基类、 等) 的给定对象。 


**扩展方法**

如前文所述，模型对象的行为非常类似于 JavaScript 对象和其原型链。 除了表示给定 IModelObject 接口的实例，可能有任意数目的父模型附加到对象 （其中每个可能，又具有任意数量的附加到它们的父模型）。 这是数据模型中的可扩展性的主要方式。 如果给定的属性或概念找不到给定实例中，会执行深度优先搜索 （由父模型定义） 的对象树的根节点的实例。 

以下方法操作与给定 IModelObject 实例相关联的父模型链： 

```cpp
STDMETHOD(GetNumberOfParentModels)(_Out_ ULONG64* numModels) PURE;
STDMETHOD(GetParentModel)(_In_ ULONG64 i, _COM_Outptr_ IModelObject **model, _COM_Outptr_result_maybenull_ IModelObject **contextObject) PURE;
STDMETHOD(AddParentModel)(_In_ IModelObject* model, _In_opt_ IModelObject* contextObject, _In_ bool override) PURE;
STDMETHOD(RemoveParentModel)(_In_ IModelObject* model) PURE;
STDMETHOD(SetContextForDataModel)(_In_ IModelObject* dataModelObject, _In_ IUnknown* context) PURE;
STDMETHOD(GetContextForDataModel)(_In_ IModelObject* dataModelObject, _Out_ IUnknown** context) PURE;
```

[GetNumberOfParentModels](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getnumberofparentmodels)

GetNumberOfParentModels 方法返回父模型附加到给定的对象实例的数。 父模型中属性的父模型链的线性排序中的深度优先搜索。 

[GetParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getparentmodel)

GetParentModel 方法返回在给定对象的父模型链中的第 i 个父模型。 父模型中搜索的属性或添加或枚举的线性顺序中的概念。 在具有索引的父模型之前 （按层次结构） 搜索索引 i 为零的父模型。 

[AddParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-addparentmodel)

AddParentModel 方法将新的父模型添加到给定的对象。 （重写参数指定为 false） 的搜索链末尾或搜索链 （重写参数指定为 true） 的正面，可能会添加这种模型。 此外，每个父模型可能会选择性地调整上下文 (语义此指针) 的任何属性或在给定的父 （或其父层次结构中的任何人） 的概念。 上下文调整很少使用，但允许某些功能强大的概念，如对象嵌入，构造的命名空间，等等... 

[RemoveParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-removeparentmodel)

RemoveParentModel 将从给定对象的父搜索链中删除指定的父模型。 

[SetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setcontextfordatamodel)

数据模型的实现使用 SetContextForDataModel 方法实现数据放置在实例对象。 从概念上讲，每个 IModelObject （我们称之为该实例为简单起见） 包含状态的哈希表。 由另一个 IModelObject （调用此数据模型为简单起见） 是该实例的父模型层次结构中编制索引的哈希表。 此哈希值中包含的值是引用的一组计数 IUnknown 实例所表示的状态信息。 当数据模型的实例上设置此状态后它可以存储任意实现数据等属性 getter 时，可以检索这些数据。 

[GetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getcontextfordatamodel)

GetContextForDataModel 方法用于检索与 SetContextForDataModel 调用之前设置上下文信息。 这将检索状态信息的数据模型设置的实例对象上该实例对象的父模型层次结构中。 有关此上下文/状态和及其含义的更多详细信息，请参阅 SetContextForDataModel 的文档。 




## <a name="span-idobjecttypesspan-debugger-data-model-core-object-types"></a><span id="objecttypes"></span> 调试器数据模型核心对象类型


数据模型中的对象是对象的在.NET 中的概念类似。 它是可以在其中装箱数据模型能够理解的构造的泛型容器。 除了本机对象和综合 （动态） 对象，还有一系列的核心对象类型可以是放置 （或装箱） 到 IModelObject 容器。 大多数这些值放置在该域中的容器是一种标准 COM/OLE variant 类型的值与大量其他限制提出该变体可以包含的内容。 其中的最基本类型包括：

- 8 位无符号和带符号的值 （VT_UI1、 VT_I1）
- 16 位无符号和带符号的值 （VT_UI2、 VT_UI2）
- 32 位无符号和带符号的值 （VT_UI4、 VT_I4）
- 64 位无符号和带符号的值 （VT_UI8、 为 VT_I8）
- 单精度和双精度浮点值 （VT_R4，VT_R8）
- 字符串 (VT_BSTR)
- 布尔值 (VT_BOOL)

除了这些基本类型的多个核心数据模型对象放入 IModelObject VT_UNKNOWN 其中保证存储的 IUnknown 实现特定接口定义中。 这些类型包括： 

- 属性访问器 (IModelPropertyAccessor)
- 方法的对象 (IModelMethod)
- 键引用对象 （IModelKeyReference 或 IModelKeyReference2）
- 上下文对象 (IDebugModelHostContext)

**属性访问器：*IModelPropertyAccessor***

数据模型中的属性访问器是装箱到 IModelObject IModelPropertyAccessor 接口的实现。 模型对象将返回一种类型的 ObjectPropertyAccessor 查询时，内部函数的值为 VT_UNKNOWN 这可保证为 IModelPropertyAccessor 的可查询。 在过程中，它被保证可静态强制转换为 IModelPropertyAccessor。 

属性访问器是用于获取和设置密钥值的数据模型中获取方法调用的间接方法。 如果给定的键的值为属性访问器，GetKeyValue 和 SetKeyValue 方法将自动发现此问题，并调用适当属性访问器的基础 GetValue 或 SetValue 方法。 

IModelPropertyAccessor 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IModelPropertyAccessor, IUnknown)
{
    STDMETHOD(GetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _COM_Outptr_ IModelObject** value) PURE;
    STDMETHOD(SetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _In_ IModelObject* value) PURE; 
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-getvalue)

GetValue 方法是属性访问器的 getter。 只要客户端想要提取的属性的基础值，则会调用它。 请注意，它可直接获取属性访问器的任何调用方负责将密钥名称和准确的实例对象 （此指针） 传递给属性访问器的 GetValue 方法。 

[SetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-setvalue)

SetValue 方法是属性访问器的资源库。 只要客户端想要将值分配给基础属性会调用它。 许多属性都是只读的。 在这种情况下，调用 SetValue 方法将返回 E_NOTIMPL。 请注意，它可直接获取属性访问器的任何调用方负责向属性访问器的 SetValue 方法传递密钥名称和准确的实例对象 （此指针）。 


**方法：*IModelMethod***

数据模型中的方法是装箱到 IModelObject IModelMethod 接口的实现。 模型对象将返回一种类型的 ObjectMethod 查询时，内部函数的值为 VT_UNKNOWN 这可保证为 IModelMethod 的可查询。 在过程中，它被保证可静态强制转换为 IModelMethod。 数据模型中的所有方法都是动态性质。 它们采用作为输入一组 0 或更多参数，并返回单个输出值。 没有任何重载决策和参数名称、 类型或期望有关的任何元数据。 

IModelMethod 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IModelMethod, IUnknown)
{
    STDMETHOD(Call)(_In_opt_ IModelObject *pContextObject, _In_ ULONG64 argCount, _In_reads_(argCount) IModelObject **ppArguments, _COM_Errorptr_ IModelObject **ppResult, _COM_Outptr_opt_result_maybenull_ IKeyStore **ppMetadata) PURE;
}
```

[Call](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelmethod-call)

调用方法是在数据中定义的任何方法中调用模型的方法。 调用方负责进行传递的准确实例对象 （此指针） 和一组任意的参数。 返回的结果，该方法和与该结果关联的任何可选元数据。 仍以逻辑方式不会返回一个值的方法必须返回有效 IModelObject。 在这种情况下，IModelObject 是一个装箱没有值。 如果方法失败，它可能可选扩展的错误信息返回输入参数中 （即使返回的 HRESULT 是失败）。 则必须对此检查调用方。 


**键的引用：*IModelKeyReference 或 IModelKeyReference2***

从本质上讲，键引用是对特定对象上的某个键的句柄。 客户端可以检索此类通过 GetKeyReference 之类的方法的句柄和更高版本使用的句柄，以获取或设置键的值而不一定保留于该原始对象。 此类型是对象的装箱到 IModelObject IModelKeyReference 或 IModelKeyReference2 接口的实现。 模型对象将返回一种类型的 ObjectKeyReference 查询时，然后内部函数的值为 VT_UNKNOWN 这可保证为 IModelKeyReference 的可查询。 在过程中，它被保证可静态强制转换为 IModelKeyReference。 

键引用接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IModelKeyReference2, IModelKeyReference)
{
    STDMETHOD(GetKeyName)(_Out_ BSTR* keyName) PURE;
    STDMETHOD(GetOriginalObject)(_COM_Outptr_ IModelObject** originalObject) PURE;
    STDMETHOD(GetContextObject)(_COM_Outptr_ IModelObject** containingObject) PURE;
    STDMETHOD(GetKey)(_COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(GetKeyValue)(_COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetKey)(_In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
    STDMETHOD(SetKeyValue)(_In_ IModelObject* object) PURE;
    STDMETHOD(OverrideContextObject)(_In_ IModelObject* newContextObject) PURE;
}
```

[GetKeyName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyname)

GetKeyName 方法将返回到此键的引用是一个句柄的密钥的名称。 返回的字符串是标准的 BSTR，必须通过调用 SysFreeString 释放。 

[GetOriginalObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getoriginalobject)

GetOriginalObject 方法返回从其创建键引用的实例对象。 请注意，该密钥本身可能就是在实例对象的父模型。 

[GetContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getcontextobject)

GetContextObject 方法返回的上下文 （此指针） 将传递给属性访问器的 GetValue 或 SetValue 方法中，如果有问题的键所引用的属性访问器。 此处返回的上下文对象可能也可能不是从 GetOriginalObject 中提取的原始对象相同。 如果密钥在父模型，并且没有与该父模型相关联的上下文精算师，原始对象是在其调用 GetKeyReference 或 EnumerateKeyReferences 的实例对象。 上下文对象将任何不再是最终上下文精算师原始对象与包含此键的引用是一个句柄的密钥的父模型之间。 如果不有任何上下文理，原始对象和上下文对象均相同。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkey)

上的键引用的 GetKey 方法的行为像 IModelObject GetKey 方法一样。 它返回基础密钥和任何与键关联的元数据的值。 如果键的值恰好是属性访问器，这将返回到 IModelObject 装箱的属性访问器 (IModelPropertyAccessor)。 此方法不会在属性访问器上调用基础的 GetValue 或 SetValue 方法。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyvalue)

上的键引用的 GetKeyValue 方法的行为像 IModelObject GetKeyValue 方法一样。 它返回基础密钥和任何与键关联的元数据的值。 如果键的值恰好是属性访问器，这将自动调用属性访问器上的基础的 GetValue 方法。 


[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-setkey)

上的键引用的 setkey 权限方法的行为像 IModelObject 的 setkey 权限方法一样。 它将指定键的值。 如果将原始密钥属性访问器，这将替换属性访问器。 它将在属性访问器上调用 SetValue 方法。 


[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-setkeyvalue)

上的键引用的 SetKeyValue 方法的行为像 IModelObject SetKeyValue 方法一样。 它将指定键的值。 如果将原始密钥属性访问器，这将属性访问器，而无需替换为属性访问器本身上调用基础的 SetValue 方法。 

[OverrideContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference2-overridecontextobject)

OverrideContextObject 方法 （仅提供 IModelKeyReference2 上） 是一个高级的方法，它用于永久更改此键的引用将传递到任何基础的属性访问器的 GetValue 或 SetValue 方法的上下文对象。 此外将通过调用 GetContextObject 返回传递给此方法的对象。 此方法可以由脚本提供程序，用于复制某些动态语言行为。 大多数客户端不应调用此方法。 


**上下文对象：*IDebugHostContext***

上下文对象都是信息的不透明 blob 的调试主机 （位于数据模型与协作） 相关联的每个对象。 它可能包括等进程的上下文或地址空间的信息来自等内容...上下文对象是 IDebugHostContext 内 IModelObject 装箱的实现。 请注意，IDebugHostContext 主机定义接口。 客户端将永远不会实现此接口。 

有关上下文对象的详细信息，请参阅[调试器的数据模型 c + + 主机接口](data-model-cpp-interfaces.md#hostinterface)中调试器的数据模型 c + + 接口。 


## <a name="span-idmodelmanager-the-data-model-manager"></a><span id="modelmanager"> 数据模型管理器  

向数据模型管理，IDataModelManager2 （或更早 IDataModelManager） 的核心接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDataModelManager2, IDataModelManager)
{
    //
    // IDataModelManager:
    //
    STDMETHOD(Close)() PURE;
    STDMETHOD(CreateNoValue)(_Out_ IModelObject** object) PURE;
    STDMETHOD(CreateErrorObject)(_In_ HRESULT hrError, _In_opt_ PCWSTR pwszMessage, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateTypedObject)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(CreateTypedObjectReference)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
    STDMETHOD(CreateSyntheticObject)(_In_opt_ IDebugHostContext* context, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateDataModelObject)(_In_ IDataModelConcept* dataModel, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateIntrinsicObject)(_In_ ModelObjectKind objectKind, _In_ VARIANT* intrinsicData, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(CreateTypedIntrinsicObject)(_In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
    STDMETHOD(GetModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ IModelObject** dataModel) PURE;
    STDMETHOD(GetModelForType)(_In_ IDebugHostType* type, _COM_Outptr_ IModelObject** dataModel, _COM_Outptr_opt_ IDebugHostTypeSignature** typeSignature, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(RegisterModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterModelForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(RegisterExtensionForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterExtensionForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(CreateMetadataStore)(_In_opt_ IKeyStore* parentStore, _COM_Outptr_ IKeyStore** metadataStore) PURE;
    STDMETHOD(GetRootNamespace)(_COM_Outptr_ IModelObject** rootNamespace) PURE;
    STDMETHOD(RegisterNamedModel)(_In_ PCWSTR modelName, _In_ IModelObject *modeObject) PURE;
    STDMETHOD(UnregisterNamedModel)(_In_ PCWSTR modelName) PURE;
    STDMETHOD(AcquireNamedModel)(_In_ PCWSTR modelName, _COM_Outptr_ IModelObject **modelObject) PURE;
    //
    // IDataModelManager2:
    //
    STDMETHOD(AcquireSubNamespace)(_In_ PCWSTR modelName, _In_ PCWSTR subNamespaceModelName, _In_ PCWSTR accessName, _In_opt_ IKeyStore *metadata, _COM_Outptr_ IModelObject **namespaceModelObject) PURE;
    STDMETHOD(CreateTypedIntrinsicObjectEx)(_In_opt_ IDebugHostContext* context, _In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
}
```

**管理方法**

以下组的方法使用的应用程序 (例如： 调试器) 托管的数据模型。 

```cpp
STDMETHOD(Close)() PURE;
```

[关闭](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-close)

通过应用程序数据模型管理器上调用 Close 方法 (例如： 调试器) 若要启动的数据模型管理器的关闭进程中承载的数据模型。 这会执行未在释放它的数据模型管理器中的最后一个引用之前的 Close 方法的数据模型的主机可能会导致未定义的行为包括，但不是限于数据模型的管理基础结构的重要泄漏。 

**对象创建 / 装箱方法**

以下组方法用于创建新对象或框值到 IModelObject-数据模型的核心接口。 

```cpp
STDMETHOD(CreateNoValue)(_Out_ IModelObject** object) PURE;
STDMETHOD(CreateErrorObject)(_In_ HRESULT hrError, _In_opt_ PCWSTR pwszMessage, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateTypedObject)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(CreateTypedObjectReference)(_In_opt_ IDebugHostContext* context, _In_ Location objectLocation, _In_ IDebugHostType* objectType, _COM_Errorptr_ IModelObject** object) PURE;
STDMETHOD(CreateSyntheticObject)(_In_opt_ IDebugHostContext* context, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateDataModelObject)(_In_ IDataModelConcept* dataModel, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateIntrinsicObject)(_In_ ModelObjectKind objectKind, _In_ VARIANT* intrinsicData, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateTypedIntrinsicObject)(_In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
STDMETHOD(CreateMetadataStore)(_In_opt_ IKeyStore* parentStore, _COM_Outptr_ IKeyStore** metadataStore) PURE;
STDMETHOD(CreateTypedIntrinsicObjectEx)(_In_opt_ IDebugHostContext* context, _In_ VARIANT* intrinsicData, _In_ IDebugHostType* type, _COM_Outptr_ IModelObject** object) PURE;
```

[CreateNoValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createnovalue)

CreateNoValue 方法创建的"no value"对象、 到 IModelObject 框并将其返回。 返回的模型对象具有一种类型的 ObjectNoValue。 

"No value"对象具有多个语义含义如下： 

- （具体取决于语言），它可被视为 void、 空或未定义的语义等效项
- 这将返回成功和生成"no value"对象的任何属性访问器的 GetValue 方法指示特定属性的给定实例没有值并且应视为如同该属性不存在为该特定实例。
- 在语义上不具有返回值的数据模型方法使用它作为 sentinel 来表明此类 （如方法必须返回有效 IModelObject）。

[CreateErrorObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createerrorobject)

CreateErrorObject 方法创建一个"error 对象"。 数据模型不具有异常和异常流的概念。 故障不再是两种方法中的属性/方法：

- 一个与任何扩展的错误信息失败的 HRESULT。 没有可以提供错误的详细信息，或者与错误本身都简单易懂，从返回的 HRESULT。
- 单个失败的 HRESULT 再加上扩展错误信息。 扩展的错误信息是属性/方法的输出参数中返回的错误对象。

[CreateTypedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobject)

CreateTypedObject 方法是允许客户端在调试目标的地址空间中创建本机/语言对象的表示形式的方法。 如果新创建的对象 （即对象类型参数） 的类型恰好匹配一个或多个类型签名作为规范的可视化工具或扩展注册到数据模型管理器，这些匹配的数据模型会自动将返回给调用方之前，附加到创建的实例对象。 

[CreateTypedObjectReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobjectreference)

CreateTypedObjectReference 方法是在语义上类似于 CreateTypedObject 方法，只不过它创建对基础本机/语言构造的引用。 创建的引用的是具有一种类型的 ObjectTargetObjectReference 的对象。 它不是因为基础语言可能支持的本机引用 (例如： c + + （& a) 或 & &)。 它是完全可能有 ObjectTargetObjectReference 为 c + + 引用。 类型 ObjectTargetObjectReference 对象可以转换为通过使用 IModelObject 上的取消引用方法的基础值。 该引用还可以传递到基础主机的表达式计算器以便将分配后一种语言中的值为适当的方式。 

[CreateSyntheticObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createsyntheticobject)

CreateSyntheticObject 方法创建空的数据模型对象-元数据键/值元组和概念的字典。 在创建时，没有密钥也不在对象上的概念。 它是调用方能够利用在干净状态。 

[CreateDataModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createdatamodelobject)

CreateDataModelObject 方法是简单的帮助程序包装创建对象的数据模型--是要作为父模型连接到其他对象的对象。 所有这类对象必须支持通过 IDataModelConcept 的数据模型概念。 此方法没有显式的上下文中创建一个新的空白综合对象，并将 inpassed 的 IDataModelConcept 添加为新创建的对象实现的数据模型概念。 这同样可以获得对 CreateSyntheticObject 和 SetConcept 的调用。 

[CreateIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createintrinsicobject)

CreateIntrinsicObject 方法是到 IModelObject 框内部值的方法。 调用方将该值放在 COM 变体，并调用此方法。 数据模型管理器将返回该对象表示 IModelObject。 请注意此方法也使用基本的基于 IUnknown 类型进行装箱： 属性访问器、 方法、 上下文、 等等...在这种情况下，objectKind 方法指示哪种基于 IUnknown 构造该对象表示和所传递变量 punkVal 字段是 IUnknown 派生类型。 类型必须是静态强制转换为适当的模型接口 (例如：IModelPropertyAccessor、 IModelMethod、 IDebugHostContext，等等。...)在过程。 此方法支持的变体类型是 VT_UI1、 VT_I1、 VT_UI2、 VT_I2、 VT_UI4、 VT_I4、 VT_UI8、 为 VT_I8、 VT_R4、 VT_R8、 VT_BOOL、 VT_BSTR、 和 VT_UNKNOWN （适用于 IUnknown 派生类型由枚举 ModelObjectKind 专用的一组。 

[CreateTypedIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedintrinsicobject)

CreateTypedintrinsicObject 方法是类似于 CreateIntrinsicObject 方法，只不过它允许本机/语言类型，以与数据关联和装箱的值一起传送。 这样可让数据模型来表示构造，如本机枚举类型 （它们是只需 VT_UI * 或 VT_I * 的值）。 指针类型还会使用此方法创建。 数据模型中的本机指针是零扩展的 64 位的数量到调试目标的虚拟地址空间表示某一偏移量。 它在 VT_UI8 装箱，并使用此方法，并指示本机/语言指针的类型创建。 

[CreateMetadataStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createmetadatastore)

CreateMetadataStore 方法创建用来保存与属性和各种其他值相关联的元数据的密钥存储-简化容器的元数据键/值元组。 元数据存储区可能有一个父代 （这反过来会产生单一父）。 如果给定的元数据密钥不在给定存储区中，将检查其父项。 大多数元数据存储不具有父级。 但是，提供一种方法轻松地共享公共元数据。 

[CreateTypedIntrinsicObjectEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager2-createtypedintrinsicobjectex)

CreateTypedIntrinsicObjectEx 方法是在语义上类似于 CreateTypedIntrinsicObject 方法。 两者之间唯一的区别是，此方法允许调用方指定的上下文内部的数据无效。 如果未不传递任何上下文，数据被视为在从 （CreateTypedIntrinsicObject 行为方式） 的类型参数继承任何上下文中有效。 这允许创建的类型化的指针值中的调试目标需要更多特定上下文不是可以从该类型继承。 

**可扩展性 / 注册方法**以下一组的方法管理数据模型，从而允许客户端扩展或注册现有模型或询问要自动将给定的父模型连接上的数据模型的扩展性机制这与给定的条件匹配的本机类型。

```cpp
    STDMETHOD(GetModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ IModelObject** dataModel) PURE;
    STDMETHOD(GetModelForType)(_In_ IDebugHostType* type, _COM_Outptr_ IModelObject** dataModel, _COM_Outptr_opt_ IDebugHostTypeSignature** typeSignature, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(RegisterModelForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterModelForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(RegisterExtensionForTypeSignature)(_In_ IDebugHostTypeSignature* typeSignature, _In_ IModelObject* dataModel) PURE;
    STDMETHOD(UnregisterExtensionForTypeSignature)(_In_ IModelObject* dataModel, _In_opt_ IDebugHostTypeSignature* typeSignature) PURE;
    STDMETHOD(GetRootNamespace)(_COM_Outptr_ IModelObject** rootNamespace) PURE;
    STDMETHOD(RegisterNamedModel)(_In_ PCWSTR modelName, _In_ IModelObject *modeObject) PURE;
    STDMETHOD(UnregisterNamedModel)(_In_ PCWSTR modelName) PURE;
    STDMETHOD(AcquireNamedModel)(_In_ PCWSTR modelName, _COM_Outptr_ IModelObject **modelObject) PURE;
```

[GetModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortypesignature)

GetModelForTypeSignature 方法将返回针对特定类型签名通过 RegisterModelForTypeSignature 方法调用之前已注册的数据模型。 此方法返回的数据模型被视为与传递的类型签名匹配的任何类型的规范可视化工具。 作为规范的可视化工具，该数据模型将于类型的显示。 显示引擎默认情况下，将隐藏而提供的数据模型的对象的视图对象的本机/语言构造。 


[GetModelForType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortype)

GetModelForType 方法返回的数据模型，它是给定的类型实例的规范可视化工具。 实际上，此方法查找最匹配的类型签名 RegisterModelForTypeSignature 方法调用之前已注册并返回关联的数据模型。 

[RegisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-registermodelfortypesignature)

RegisterModelForTypeSignature 方法是调用方使用注册给定类型 （或组的类型） 的规范可视化工具的主要方法。 规范的可视化工具是有效时，将给定的类型 （或组的类型） 显示于数据模型。 而不是在调试器用户界面中显示的类型本机/语言视图中，为已注册的数据模型提供的类型的视图显示 （以及取回到需要它的用户的本机/语言视图的方法）。 

[UnregisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregistermodelfortypesignature)

UnregisterModelForTypeSignature 方法撤消 RegisterModelForTypeSignature 方法调用之前。 此方法可以删除给定的数据模型作为规范的可视化工具类型匹配的特定类型签名或它可以为每个在其下注册了该数据模型的类型签名的规范可视化工具中删除给定的数据模型。 

[RegisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-registerextensionfortypesignature)

RegisterExtensionForTypeSignature 方法是类似于 RegisterModelForTypeSignature 方法有一个重大差异。 数据模型传递给此方法不是任何类型的规范可视化工具，它将不会对该类型的本机/语言视图的显示。 数据模型传递给此方法将自动添加作为父级到与提供的类型签名匹配的任何具体类型。 与 RegisterModelForTypeSignature 方法不同的注册为给定的类型 （或组的类型） 的扩展的相同或不明确的类型签名上没有任何限制。 每个类型签名与给定的具体类型实例相匹配的扩展将导致通过此方法以自动附加到父模型为新创建的对象注册的数据模型。 此操作，实际上，允许任意数目的客户端以使用新的字段或功能进行扩展的类型 （或组的类型）。 

[UnregisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisterextensionfortypesignature)

UnregisterExtensionForTypeSignature 方法撤消 RegisterExtensionForTypeSignature 调用之前。 用作特定类型签名的扩展或作为数据模型已针对其注册的所有类型签名的扩展，它会注销特定数据模型。 

[GetRootNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

GetRootNamespace 方法返回的数据模型的根命名空间。 这是一个对象，它的数据模型管理和调试主机将某些对象放置到其中。 

[RegisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

RegisterNamedModel 方法注册为给定的数据模型在已知的名称，以便可通过客户端希望对其进行扩展。 这是 API-发布可以通过检索此已知名称下注册的模型来扩展数据模型作为内容的主要用途并向其中添加父模型。 

[UnregisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisternamedmodel)

UnregisterNamedModel 方法撤消 RegisterNamedModel 调用之前。 它删除数据模型和在其下它可以查找的名称之间的关联。 

[AcquireNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-acquirenamedmodel)

调用方想要扩展数据模型的具有给定名称注册时调用 AcquireNamedModel 方法以检索他们想要扩展的数据模型的对象。 此方法将返回通过 RegisterNamedModel 方法调用之前注册了任何数据模型。 由于 AcquireNamedModel 方法的主要目的是要扩展模型，此方法将具有特殊行为，如果尚未已使用给定名称注册了任何模型。 如果没有模型具有尚未注册给定的名称下，存根 （stub） 对象创建、 暂时下给定的名称、 注册并返回到调用方。 通过对 RegisterNamedModel 方法的调用注册的真实数据模型时，存根 （stub） 对象所做的任何更改，实际上，对实际模型。 这将从扩展每个其他组件中删除多个加载顺序依赖关系问题。 


**帮助器方法**

下面的方法是常规的帮助器方法，从而协助在执行数据模型中的对象上的复杂操作。 虽然可以在数据模型或其对象上执行这些操作通过其他方法，方便起见，这些方法可以更加便捷： 

```cpp
STDMETHOD(AcquireSubNamespace)(_In_ PCWSTR modelName, _In_ PCWSTR subNamespaceModelName, _In_ PCWSTR accessName, _In_opt_ IKeyStore *metadata, _COM_Outptr_ IModelObject **namespaceModelObject) PURE;
```

[AcquireSubNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager2-acquiresubnamespace)

AcquireSubNamespace 方法可帮助更传统上可能看起来是语言命名空间比动态语言中的新对象的内容构造中。 如果，例如，调用方想要将进程对象，从而使更有条理的进程对象的属性和更轻松地发现，这样做这就是创建每个类别的子对象上的进程对象并将放入的一种方法的属性分类该对象内的这些属性。 




---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[调试程序数据模型 c + + 概述](data-model-cpp-overview.md)

[调试器数据模型 c + + 接口](data-model-cpp-interfaces.md)

[调试器数据模型 c + + 对象](data-model-cpp-objects.md)

[调试器数据模型 c + + 其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 c + + 概念](data-model-cpp-concepts.md)

[C + + 编写脚本的调试程序数据模型](data-model-cpp-scripting.md)
