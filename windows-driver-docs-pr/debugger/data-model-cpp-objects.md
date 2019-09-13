---
title: 调试器数据模型 C++ 对象
description: 本主题介绍如何使用调试器数据模型C++对象，以及如何扩展调试器的功能。
ms.date: 09/12/2019
ms.openlocfilehash: 6f124666cf8424080b8bddd93bce6efd4e948263
ms.sourcegitcommit: 3b7c8b3cb59031e0f4e39dac106c1598ad108828
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2019
ms.locfileid: "70930375"
---
# <a name="debugger-data-model-c-objects"></a>调试器数据模型 C++ 对象

本主题介绍如何使用调试器数据模型C++对象，以及如何扩展调试器的功能。

## <a name="span-idcore--the-core-debugger-object-model"></a><span id="core">核心调试器对象模型

数据模型的最基本但功能最强大的功能之一是，它标准化对象的定义以及一个对象与对象交互的方式。 *IModelObject*接口封装对象的概念，无论对象是整数、浮点值、字符串、调试器的目标地址空间中的某些复杂类型还是某些调试器概念（如进程的概念或模块.

有几个不同的内容可以保留在*IModelObject*中（或装箱入）：

-   **内部值**- *IModelObject*可以是多个基本类型的容器：8、16、32或64位有符号或无符号整数、布尔值、字符串、错误或概念为空。

-   **本机对象**- *IModelObject*可以表示调试器的类型系统所定义的复杂类型（如调试器的类型系统所定义），无论调试器的目标是什么 
    
-   **合成对象**- *IModelObject*可以是动态对象--字典（如果要执行此操作）：一个键/值/元组和一组概念，这些**概念**定义不只由键/值对表示的行为。

-   **Properties** - *IModelObject*可表示属性：可以使用方法调用来检索或更改其值的某些内容。 *IModelObject*中的属性实际上是封装为*IModelObject*的*IModelPropertyAccessor*接口。

-   **方法**- *IModelObject*可表示方法：可以使用一组参数调用的某些内容并获取返回值。 *IModelObject*中的方法实际上是封装为*IModelObject*的*IModelMethod*接口。

### <a name="extensibility-within-the-object-model"></a>对象模型中的扩展性

*IModelObject*不是隔离的对象。 除了表示上面所示的对象类型之一，每个对象都具有父数据模型链的概念。 此链的行为与[JavaScript 原型链](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)非常类似。
每个数据模型对象定义一个**父模型**的线性链，而不是 JavaScript 这样的原型的线性链。 其中的每个父模型反过来都具有自己的一组父模型的另一个线性链。 实质上，每个对象都是此树中本身和每个对象的功能（属性等）的聚合。 查询特定属性时，如果对其进行查询的对象不支持该属性，则查询将以线性顺序传递到每个父级。 这会创建一个行为，在此行为中，将通过对聚合树进行深度优先搜索来解析属性。

此对象模型中的扩展性非常简单，因为这种情况下，每个对象都是其自身和父模型树的聚合。 扩展可以进入并添加到另一个对象的父模型列表。 执行此操作将**扩展**对象。 通过这种方式，可以将功能添加到任何项目：对象或值的特定实例、本机类型、进程或线程的概念，甚至是 "所有可迭代对象" 的概念。

### <a name="context-context-and-context-the-this-pointer-the-address-space-and-implementation-private-data"></a>上下文、上下文和上下文：**This**指针、地址空间和实现专用数据

有三种**上下文**需要了解对象模型的上下文中。

#### <a name="context-the-this-pointer"></a>上下文：**This**指针

由于给定的属性或方法可能在数据模型树的任何级别实现，因此，实现方法或属性必须能够访问原始对象（您可能会在或此中C++调用**this**指针**JavaScript 中的 c2 > 对象。** 在所述的方法中，将该实例对象传递到各种方法，作为名为**上下文**的第一个参数。

#### <a name="context-the-address-space"></a>上下文：地址空间

需要注意的一点是，与先前的扩展模型不同的是，**上下文**（目标、进程、您正在查看的线程）的 UI 概念与所有 api 相对于当前 ui 状态，数据模型接口通常显式采用此上下文或隐式为*IDebugHostContext*接口。 数据模型中的每个*IModelObject*都附带此类型的上下文信息，并可以将该上下文传播到它返回的对象。 这意味着，当你从*IModelObject*读取本机值或键值时，它将从最初从中获取对象的目标和进程中读出。

有一个显式常数值，可**使用\_当前\_宿主\_上下文**，该上下文可传递到采用*IDebugHostContext*参数的方法。 此值指示上下文确实是调试器的当前 UI 状态。 但这种概念需要是显式的。

#### <a name="context-implementation-private-data"></a>上下文：实现专用数据

请记住，数据模型中的每个对象实际上是对象实例和附加的父模型树的聚合。
其中的每个父模型（可在许多不同对象的链中链接）可以将私有实现数据与任何实例对象相关联。 在概念上创建的每个*IModelObject*都有一个哈希表，该表将特定父模型映射到*IUnknown*接口定义的专用实例数据。 这允许父模型缓存每个实例上的信息，或者有其他任意关联的数据。

通过*IModelObject*上的*GetContextForDataModel*和*SetContextForDataModel*方法访问此类型的上下文。




## <a name="span-idimodelobjectspan-the-core-debugger-object-interface-imodelobject"></a><span id="imodelobject"></span>核心调试器对象接口：**IModelObject**

-------------------------------------------

*IModelObject*接口定义如下：

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

下面是适用于 IModelObject 所表示的任何类型的对象的一般方法。 

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

GetKind 方法返回 IModelObject 内装箱的对象类型。 

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getcontext)

GetContext 方法返回与对象关联的主机上下文。 

[GetIntrinsicValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getintrinsicvalue)

GetIntrinsicValue 方法返回在 IModelObject 内装箱的内容。 此方法只能在 IModelObject 接口上调用，后者表示装箱的内部函数或装箱的特定接口。 不能对本机对象、值对象、合成对象和引用对象调用此方法。 GetIntrinsicValueAs 方法的行为与 GetIntrinsicValue 方法的行为非常相似，只不过将值转换为指定的变量类型。 如果无法执行转换，该方法将返回错误。

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-isequalto)

IsEqualTo 方法比较两个模型对象，并返回值中是否相等。 对于具有排序的对象，此方法返回 true 等效于比较方法返回0。 对于没有排序但是可相等的对象，Compare 方法将失败，但这不会失败。 基于值的比较的含义由对象的类型定义。 目前只为内部类型和错误对象定义了这种情况。 没有适用于 equatability 的当前数据模型概念。 

[取消引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-dereference)

取消引用方法取消引用对象。 此方法可用于取消引用基于数据模型的引用（ObjectTargetObjectReference、ObjectKeyReference）或本机语言引用（指针或语言引用）。 请务必注意，此方法会在对象上删除单个级别的引用语义。 例如，完全可以对语言引用进行数据模型引用。 在这种情况下，第一次调用取消引用方法将删除数据模型引用并保留语言引用。 对此生成的对象调用取消引用后，将删除语言引用并返回该引用下的本机值。 


**键操作方法**

作为键、值和元数据元组的字典的任何合成对象都具有一系列方法来操作这些键、值以及与它们关联的元数据。 

Api 的基于值的形式为： 

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

Api 基于引用的形式为： 

```cpp
STDMETHOD(GetKeyReference)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** objectReference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
STDMETHOD(EnumerateKeyReferences)(_COM_Outptr_ IKeyEnumerator** enumerator) PURE;
```

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkeyvalue)

GetKeyValue 方法是客户端将转换为的第一种方法，以便按名称获取（以及与相关联的元数据）的值。 如果该键是属性访问器（这是一个装箱 IModelPropertyAccessor 的 IModelObject），则 GetKeyValue 方法会自动调用属性访问器的 GetValue 方法，以便检索实际值。

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setkeyvalue)

SetKeyValue 方法是客户端将转换为的第一种方法，以便设置键的值。 此方法不能用于在对象上创建新键。 它只会设置现有密钥的值。 请注意，许多键是只读的（例如：它们是通过属性访问器实现的，该访问器从其 SetValue 方法返回 E_NOT_IMPL）。 对只读密钥调用此方法时，此方法将失败。 

[EnumerateKeyValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyvalues)

EnumerateKeyValues 方法是客户端将转换为的第一种方法，以便枚举对象上的所有键（包括父模型树中任何位置实现的所有键）。 请务必注意，EnumerateKeyValues 将枚举对象树中的重复名称定义的任何密钥;但是，GetKeyValue 和 SetKeyValue 之类的方法只会操作具有给定名称的键的第一个实例，如深度优先遍历所发现。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkey)

GetKey 方法将按名称获取给定键的值（以及与相关联的元数据）。 大多数客户端应使用 GetKeyValue 方法。 如果该键是属性访问器，则调用此方法会将属性访问器（IModelPropertyAccessor 接口）返回装箱为 IModelObject。 与 GetKeyValue 不同，此方法不会通过调用 GetValue 方法自动解析密钥的基础值。 这是调用方的责任。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setkey)

SetKey 方法是客户端将转换为的方法，以便为对象创建密钥（并且可能会将元数据与创建的密钥关联）。 如果给定的对象已有具有给定名称的键，则会出现两种情况之一。 如果该键在此给定的实例上，则将替换该密钥的值，就像原始密钥不存在一样。 另一方面，如果该键位于由此给定的实例的父数据模型链中，则将在此给定的实例上创建具有给定名称的新键。 这实际上会导致对象具有相同名称的两个键（类似于将与基类的成员同名的派生类）。 

[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeys)

EnumerateKeys 方法的行为类似于 EnumerateKeyValues 方法只不过，但它不会自动解析对象上的属性访问器。 这意味着，如果键的值为属性访问器，则 EnumerateKeys 方法会将属性访问器（IModelPropertyAccessorInterface）返回到 IModelObject，而不是自动调用 GetValue 方法。 这类似于 "GetKey" 和 "GetKeyValue" 之间的差异。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-clearkeys)

ClearKeys 方法从此指定的对象的实例中移除所有键及其关联的值和元数据。 此方法对附加到特定对象实例的父模型不起作用。 

[GetKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getkeyreference)

GetKeyReference 方法将在对象（或其父模型链）上搜索给定名称的键，并返回对装箱到 IModelObject 的 IModelKeyReference 接口所提供的密钥的引用。 随后可使用该引用获取或设置键的值。 

[EnumerateKeyReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeratekeyreferences)

EnumerateKeyReferences 方法的行为类似于 EnumerateKeyValues 方法只不过，该方法返回对它所枚举的键的引用（由装箱到 IModelObject 中的 IModelKeyReference 接口提供），而不是键的值。 此类引用可用于获取或设置密钥的基础值。 


**概念操作方法**

除了某个模型对象是键/值/元组的字典，它还是概念的容器。 概念是可以在或对象上执行的抽象概念。 概念实质上是对象支持的接口的动态存储区。 今天的数据模型定义了许多概念： 

概念接口 | 描述
------------------|-------------
IDataModelConcept | 概念是一个父模型。 如果通过注册的类型签名将此模型自动附加到本机类型，则每次实例化此类类型的新对象时，都会自动调用 InitializeObject 方法。
IStringDisplayableConcept  | 出于显示目的，可以将对象转换为字符串。
IIterableConcept  | 对象是一个容器，可以循环访问。
IIndexableConcept  | 对象是一个容器，可以在一个或多个维度中对其进行索引（通过随机访问进行访问）。
IPreferredRuntimeTypeConcept  | 对象更详细地了解派生自它的类型，而不是基础类型系统能够提供，并希望处理其自己的从静态到运行时类型的转换。
IDynamicKeyProviderConcept | 对象是密钥的动态提供程序，希望接管核心数据模型中的所有关键查询。 此接口通常用作动态语言（如 JavaScript）的桥。
IDynamicConceptProviderConcept  | 对象是概念的动态提供程序，希望接管核心数据模型中的所有概念查询。 此接口通常用作动态语言（如 JavaScript）的桥。

IModelObject 上的以下方法可用于处理对象支持的概念。 

```cpp
STDMETHOD(GetConcept)(_In_ REFIID conceptId, _COM_Outptr_ IUnknown** conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore** conceptMetadata) PURE;
STDMETHOD(SetConcept)(_In_ REFIID conceptId, _In_ IUnknown* conceptInterface, _In_opt_ IKeyStore* conceptMetadata) PURE;
STDMETHOD(ClearConcepts)() PURE;
```

[GetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getconcept)

GetConcept 方法将在对象（或其父模型链）上搜索概念，并返回指向该概念接口的接口指针。 概念接口上的行为和方法特定于每个概念。 但请务必注意，许多概念接口要求调用方显式传递上下文对象（或通常会调用 this 指针的对象）。 务必确保将正确的上下文对象传递到每个概念接口。

[SetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setconcept)

SetConcept 方法将在由 this 指针指定的对象实例上放置指定的概念。 如果附加到由此指定的对象实例的父模型还支持该概念，则实例中的实现将重写父模型中的。 

[ClearConcepts](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-clearconcepts)

ClearConcepts 方法将从此指定的对象的实例中删除所有概念。 


**本机对象方法**

尽管许多模型对象引用内部函数（例如：整数、字符串）或综合构造（键/值/元组和概念的字典），但模型对象也可能引用本机构造（例如：调试地址空间中的用户定义类型目标）。 IModelObject 接口具有一系列方法，可访问此类本机对象的相关信息。 这些方法包括： 

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

GetRawValue 方法查找给定对象内的本机构造。 此类构造可以是字段、基类、基类中的字段、成员函数等。 

[EnumerateRawValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawvalues)

EnumerateRawValues 方法枚举给定对象的所有本机子对象（例如：字段、基类等）。 


[TryCastToRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-trycasttoruntimetype)

TryCastToRuntimeType 方法将要求调试宿主执行分析并确定给定对象的实际运行时类型（如：最派生类）。 确切的分析利用特定于调试宿主，可能包括 RTTI （C++运行时类型信息）、对对象的 "V-表" （虚拟函数表）结构的检查，或者主机可用于可靠地确定动态/静态类型中的运行时类型。 转换为运行时类型失败并不意味着此方法调用将失败。 在这种情况下，方法将在输出参数中返回给定的对象（this 指针）。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getlocation) 

GetLocation 方法将返回本机对象的位置。 尽管此类位置通常是调试目标的地址空间中的虚拟地址，但并不一定如此。 此方法返回的位置是一个抽象位置，它可以是一个虚拟地址，可以指示寄存器或子寄存器内的位置，也可以指示由调试宿主定义的其他任意地址空间。 如果生成的 Location 对象的 HostDefined 字段为0，则表示该位置实际上是一个虚拟地址。 可以通过检查产生位置的 "偏移量" 字段来检索此类虚拟地址。 HostDefined 字段的任何非零值都表示一个备用地址空间，其中偏移量字段是该地址空间内的偏移量。 此处非零 HostDefined 值的确切含义是调试宿主的专用。 

[GetTypeInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-gettypeinfo)

GetTypeInfo 方法将返回给定对象的本机类型。 如果对象不具有与其关联的本机类型信息（例如：它是内部类型，等等），则调用仍将成功，但将返回 null。 

[GetTargetInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-gettargetinfo)

GetTargetInfo 方法实际上是 GetLocation 和 GetTypeInfo 方法的组合，同时返回给定对象的抽象位置和本机类型。 

[GetRawReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getrawreference)

GetRawReference 方法在给定的对象中查找本机构造，并返回对它的引用。 此类构造可以是字段、基类、基类中的字段、成员函数等。务必将此处返回的引用（类型为 ObjectTargetObjectReference 的对象）与语言引用（例如： C++ & 或 & & 样式引用）区分开来。 

[EnumerateRawReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-enumeraterawreferences)

EnumerateRawReferences 方法枚举给定对象的所有本机子对象（例如：字段、基类等）的引用。 


**扩展性方法**

如前文所述，模型对象的行为与 JavaScript 对象及其原型链的行为非常类似。 除了指定的 IModelObject 接口所表示的实例外，可能还会有任意数目的父模型附加到该对象（反过来，每个模型都可以附加任意数量的父模型）。 这是数据模型中的可扩展性的主要方法。 如果在给定的实例中不能找到给定的属性或概念，则执行实例上以根为根的对象树的深度首次搜索。 

下面的方法操作与给定 IModelObject 实例关联的父模型链： 

```cpp
STDMETHOD(GetNumberOfParentModels)(_Out_ ULONG64* numModels) PURE;
STDMETHOD(GetParentModel)(_In_ ULONG64 i, _COM_Outptr_ IModelObject **model, _COM_Outptr_result_maybenull_ IModelObject **contextObject) PURE;
STDMETHOD(AddParentModel)(_In_ IModelObject* model, _In_opt_ IModelObject* contextObject, _In_ bool override) PURE;
STDMETHOD(RemoveParentModel)(_In_ IModelObject* model) PURE;
STDMETHOD(SetContextForDataModel)(_In_ IModelObject* dataModelObject, _In_ IUnknown* context) PURE;
STDMETHOD(GetContextForDataModel)(_In_ IModelObject* dataModelObject, _Out_ IUnknown** context) PURE;
```

[GetNumberOfParentModels](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getnumberofparentmodels)

GetNumberOfParentModels 方法返回附加到给定对象实例的父模型的数目。 在父模型链的线性排序中，将首先搜索父模型的属性深度。 

[GetParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getparentmodel)

GetParentModel 方法返回给定对象的父模型链中的第 i 个父模型。 父模型会按照添加或枚举的线性顺序在其上进行搜索。 在索引为 i + 1 的父模型之前，搜索索引为 i 为零的父模型（层次结构）。 

[AddParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-addparentmodel)

AddParentModel 方法将新的父模型添加到给定的对象。 此类模型可以添加到搜索链的末尾（override 参数被指定为 false），也可以添加到搜索链的前面（override 参数指定为 true）。 此外，对于给定父项（或其父层次结构中的任何人）的任何属性或概念，每个父模型都可以选择调整上下文（语义 this 指针）。 很少使用上下文调整，但允许使用一些功能强大的概念，如对象嵌入、构造命名空间等。 

[RemoveParentModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-removeparentmodel)

RemoveParentModel 将从给定对象的父搜索链中移除指定的父模型。 

[SetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-setcontextfordatamodel)

数据模型的实现使用 SetContextForDataModel 方法将实现数据放置在实例对象上。 从概念上讲，每个 IModelObject （为简单起见调用此实例）都包含一个状态的哈希表。 此哈希表由另一个 IModelObject （在实例的父模型层次结构中调用此数据模型）进行索引。 此哈希中包含的值是由 IUnknown 实例表示的一组引用计数的状态信息。 一旦数据模型在该实例上设置此状态，它就可以存储任意实现数据，如属性 getter 中所示。 

[GetContextForDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelobject-getcontextfordatamodel)

GetContextForDataModel 方法用于检索通过对 SetContextForDataModel 的先前调用设置的上下文信息。 这会检索在实例对象的父模型层次结构中进一步的数据模型设置的状态信息。 有关此上下文/状态及其含义的更多详细信息，请参阅 SetContextForDataModel 的文档。 




## <a name="span-idobjecttypesspan-debugger-data-model-core-object-types"></a><span id="objecttypes"></span>调试器数据模型核心对象类型


数据模型中的对象类似于 .NET 中的对象的概念。 它是可以将数据模型理解的构造装箱到的泛型容器。 除了本机对象和综合（动态）对象之外，还可以将一系列核心对象类型放置（或装箱）到 IModelObject 的容器中。 其中大部分值放置在其中的容器是标准的 COM/OLE 变体，其中有许多附加限制会置于该变量可以包含的内容上。 最基本的类型包括：

- 8位无符号值和有符号值（VT_UI1、VT_I1）
- 16位无符号值和有符号值（VT_UI2，VT_UI2）
- 32位无符号值和有符号值（VT_UI4，VT_I4）
- 64位无符号值和有符号值（VT_UI8，VT_I8）
- 单精度和双精度浮点值（VT_R4，VT_R8）
- 字符串（VT_BSTR）
- 布尔值（VT_BOOL）

除了这些基本类型外，许多核心数据模型对象还放置在由 VT_UNKNOWN 定义的 IModelObject 中，其中存储的 IUnknown 可保证实现特定接口。 这些类型包括： 

- 属性访问器（IModelPropertyAccessor）
- 方法对象（IModelMethod）
- 关键引用对象（IModelKeyReference 或 IModelKeyReference2）
- Context 对象（IDebugModelHostContext）

**属性访问器：*IModelPropertyAccessor***

数据模型中的属性访问器是封装到 IModelObject 中的 IModelPropertyAccessor 接口的实现。 查询时，模型对象将返回一种类型的 ObjectPropertyAccessor，而内部值为 VT_UNKNOWN，这是保证可用于 IModelPropertyAccessor 的查询。 在处理过程中，保证静态可转换 IModelPropertyAccessor。 

属性访问器是获取方法调用的间接方法，用于获取和设置数据模型中的键值。 如果给定键的值为属性访问器，则 GetKeyValue 和 SetKeyValue 方法将自动注意到这一点，并根据需要调用属性访问器的基础 GetValue 或 SetValue 方法。 

IModelPropertyAccessor 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IModelPropertyAccessor, IUnknown)
{
    STDMETHOD(GetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _COM_Outptr_ IModelObject** value) PURE;
    STDMETHOD(SetValue)(_In_ PCWSTR key, _In_opt_ IModelObject* contextObject, _In_ IModelObject* value) PURE; 
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-getvalue)

GetValue 方法是属性访问器的 getter。 每当客户端希望提取属性的基础值时，就会调用此方法。 请注意，直接获取属性访问器的任何调用方负责将密钥名称和准确的实例对象（this 指针）传递给属性访问器的 GetValue 方法。 

[SetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelpropertyaccessor-setvalue)

SetValue 方法是属性访问器的资源库。 每当客户端希望向基础属性分配值时，就会调用此方法。 许多属性是只读的。 在这种情况下，调用 SetValue 方法将返回 E_NOTIMPL。 请注意，直接获取属性访问器的任何调用方负责将密钥名称和准确的实例对象（this 指针）传递给属性访问器的 SetValue 方法。 


**方法*IModelMethod***

数据模型中的方法是封装到 IModelObject 中的 IModelMethod 接口的实现。 查询时，模型对象将返回一种类型的 ObjectMethod，而内部值为 VT_UNKNOWN，这是保证可用于 IModelMethod 的查询。 在处理过程中，保证静态可转换 IModelMethod。 数据模型中的所有方法都是动态的。 它们将一组0个或多个参数作为输入，并返回一个输出值。 没有重载决策，并且没有与参数名称、类型或预期有关的元数据。 

IModelMethod 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IModelMethod, IUnknown)
{
    STDMETHOD(Call)(_In_opt_ IModelObject *pContextObject, _In_ ULONG64 argCount, _In_reads_(argCount) IModelObject **ppArguments, _COM_Errorptr_ IModelObject **ppResult, _COM_Outptr_opt_result_maybenull_ IKeyStore **ppMetadata) PURE;
}
```

[Call](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelmethod-call)

Call 方法用于调用数据模型中定义的任何方法。 调用方负责传递准确的实例对象（this 指针）和任意一组参数。 返回方法和与该结果关联的任何可选元数据的结果。 不以逻辑方式返回值的方法仍必须返回有效的 IModelObject。 在这种情况下，IModelObject 是未装箱的值。 当某个方法失败时，它可能会在输入参数中返回可选的扩展错误信息（即使返回的 HRESULT 是失败）。 调用方必须检查此情况。 


**关键引用：*IModelKeyReference 或 IModelKeyReference2***

实质上，键引用是特定对象上的键的句柄。 客户端可以通过方法（如 GetKeyReference）检索此类句柄，并使用该句柄在以后获取或设置键的值，而无需保留在原始对象上。 这种类型的对象是封装到 IModelObject 的 IModelKeyReference 或 IModelKeyReference2 接口的实现。 查询后，模型对象将返回一种类型的 ObjectKeyReference，而内部值是 VT_UNKNOWN，这保证可用于 IModelKeyReference。 在处理过程中，保证静态可转换 IModelKeyReference。 

密钥引用接口定义如下： 

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

GetKeyName 方法返回此键引用所指的键的名称。 返回的字符串是标准 BSTR，必须通过调用 SysFreeString 释放。 

[GetOriginalObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getoriginalobject)

GetOriginalObject 方法返回从中创建键引用的实例对象。 请注意，键本身可能位于实例对象的父模型上。 

[GetContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getcontextobject)

如果相关键引用属性访问器，GetContextObject 方法将返回上下文（this 指针），该上下文将传递给属性访问器的 GetValue 或 SetValue 方法。 此处返回的上下文对象可能与从 GetOriginalObject 中提取的原始对象相同。 如果某个键在父模型上，并且存在与该父模型关联的上下文 adjustor，则原始对象将是调用 GetKeyReference 或 EnumerateKeyReferences 的实例对象。 上下文对象将是从原始对象和父模型（其中包含此键引用所指的键）中的最终上下文 adjustor 开始的任何内容。 如果没有上下文 adjustors，则原始对象和上下文对象是相同的。 

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkey)

键引用上的 GetKey 方法的行为与 IModelObject 上的 GetKey 方法相同。 它将返回基础键的值以及与该键关联的任何元数据。 如果键的值为属性访问器，则将返回装箱为 IModelObject 的属性访问器（IModelPropertyAccessor）。 此方法不会对属性访问器调用基础 GetValue 或 SetValue 方法。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-getkeyvalue)

键引用上的 GetKeyValue 方法的行为与 IModelObject 上的 GetKeyValue 方法相同。 它将返回基础键的值以及与该键关联的任何元数据。 如果键的值恰好为属性访问器，则这将自动调用属性访问器上的基础 GetValue 方法。 


[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-setkey)

键引用上的 SetKey 方法的行为与 IModelObject 上的 SetKey 方法相同。 它将分配密钥的值。 如果原始键是属性访问器，则将替换属性访问器。 它不会调用属性访问器上的 SetValue 方法。 


[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference-setkeyvalue)

键引用上的 SetKeyValue 方法的行为与 IModelObject 上的 SetKeyValue 方法相同。 它将分配密钥的值。 如果原始键为属性访问器，则此方法将在属性访问器上调用基础 SetValue 方法，而不是替换属性访问器本身。 

[OverrideContextObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodelkeyreference2-overridecontextobject)

OverrideContextObject 方法（仅在 IModelKeyReference2 中提供）是一个高级方法，用于永久更改此密钥引用将传递给任何基础属性访问器的 GetValue 或 SetValue 方法的上下文对象。 传递给此方法的对象也将从对 GetContextObject 的调用返回。 脚本提供程序可以使用此方法来复制某些动态语言行为。 大多数客户端不应调用此方法。 


**上下文对象：*IDebugHostContext***

上下文对象是调试宿主（与数据模型合作）关联的信息的不透明 blob。 它可能包含信息的处理上下文或地址空间等内容，等等。上下文对象是 IDebugHostContext 在 IModelObject 内的实现。 请注意，IDebugHostContext 是一个主机定义的接口。 客户端永远不会实现此接口。 

有关上下文对象的详细信息，请参阅调试器数据模型C++接口中的[调试器数据模型C++主机接口](data-model-cpp-interfaces.md#hostinterface)。 


## <a name="span-idmodelmanager-the-data-model-manager"></a><span id="modelmanager">数据模型管理器  

数据模型管理器的核心接口（IDataModelManager2 （或更早的 IDataModelManager）定义如下： 

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

以下一组方法可由承载数据模型的应用程序（例如：调试器）使用。 

```cpp
STDMETHOD(Close)() PURE;
```

[关闭](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-close)

关闭方法由承载数据模型的应用程序（例如：调试器）在数据模型管理器中调用，以便启动数据模型管理器的关闭过程。 在对数据模型管理器发布其最终引用之前，不是 Close 方法的数据模型主机可能会导致未定义的行为，包括但不限于对数据模型的管理基础结构的重大泄漏。 

**对象创建/装箱方法**

以下一组方法用于创建新对象或将 IModelObject 值到数据模型的核心接口。 

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

CreateNoValue 方法创建一个 "无值" 对象，将其装箱到 IModelObject 中，并返回该对象。 返回的模型对象的类型为 ObjectNoValue。 

"无值" 对象具有若干语义含义： 

- （根据语言），可以将其视为 void、null 或 undefined 的语义等效项
- 返回成功的任何属性访问器的 GetValue 方法和生成的 "无值" 对象指示特定属性没有给定实例的值，应将该属性视为对于该特定实例不存在。
- 不在语义上具有返回值的数据模型方法将此用作指示这种情况的 IModelObject （因为方法必须返回有效的）。

[CreateErrorObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createerrorobject)

CreateErrorObject 方法创建 "error 对象"。 数据模型不具有异常和异常流的概念。 使用以下两种方法失败：

- 不带扩展错误信息的单个失败的 HRESULT。 没有更多的信息可提供给该错误，或者错误本身从返回的 HRESULT 中一目了然。
- 与扩展的错误信息耦合的单个失败的 HRESULT。 扩展错误信息是在属性/方法的 output 参数中返回的错误对象。

[CreateTypedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobject)

CreateTypedObject 方法是允许客户端在调试目标的地址空间中创建本机/语言对象的表示形式的方法。 如果新创建的对象的类型（如 objectType 参数所示）与一个或多个注册为规范化可视化工具或扩展的数据模型管理器的类型签名相匹配，则这些匹配的数据模型将自动附加到创建的实例对象，然后将其返回给调用方。 

[CreateTypedObjectReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedobjectreference)

CreateTypedObjectReference 方法在语义上类似于 CreateTypedObject 方法只不过，它创建了对基础本机/语言构造的引用。 创建的引用是具有 ObjectTargetObjectReference 类型的对象。 它不是一种本机引用，因为基础语言可能支持（例如： C++ & 或 & &）。 完全可以将 ObjectTargetObjectReference 用于C++引用。 可以通过使用 IModelObject 上的取消引用方法，将类型 ObjectTargetObjectReference 的对象转换为基础值。 还可将引用传递到基础宿主的表达式计算器，以适当的方式将其分配给值。 

[CreateSyntheticObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createsyntheticobject)

CreateSyntheticObject 方法创建一个空的数据模型对象-一个键/值/元组和概念的字典。 创建时，对象没有任何键和概念。 这是调用方使用的一种全新的方法。 

[CreateDataModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createdatamodelobject)

CreateDataModelObject 方法是一个简单的帮助程序包装器，用于创建作为数据模型的对象，即，将作为父模型附加到其他对象的对象。 所有此类对象都必须通过 IDataModelConcept 支持数据模型概念。 此方法创建一个不带显式上下文的新的空白合成对象，并将 inpassed IDataModelConcept 添加为新创建的对象的数据模型概念实现。 同样可以通过调用 CreateSyntheticObject 和 SetConcept 来实现。 

[CreateIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createintrinsicobject)

CreateIntrinsicObject 方法是将内部值装箱到 IModelObject 的方法。 调用方将值放入 COM 变量并调用此方法。 数据模型管理器返回表示对象的 IModelObject。 请注意，此方法还用于表示基于 IUnknown 的基本类型：属性访问器、方法、上下文等。在这种情况下，objectKind 方法指示对象表示的基于 IUnknown 的构造类型，而所传递变量的 punkVal 字段是 IUnknown 派生类型。 类型必须静态地可转换到相应的模型接口（例如：IModelPropertyAccessor、 IModelMethod、 IDebugHostContext，等等...)在过程。 此方法支持的变体类型包括 VT_UI1、VT_I1、VT_UI2、VT_I2、VT_UI4、VT_I4、VT_UI8、VT_I8、VT_R4、VT_R8、VT_BOOL、VT_BSTR 和 VT_UNKNOWN （适用于枚举 ModelObjectKind 所指示的一组专用 IUnknown 派生类型）。 

[CreateTypedIntrinsicObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createtypedintrinsicobject)

CreateTypedintrinsicObject 方法类似于 CreateIntrinsicObject 方法只不过，这种方法允许将本机/语言类型与数据相关联，并与装箱值一起使用。 这允许数据模型表示构造，如本机枚举类型（只是 VT_UI * 或 VT_I * 值）。 此方法也会创建指针类型。 数据模型中的本机指针是0个扩展64位的数量，表示调试目标的虚拟地址空间的偏移量。 它在 VT_UI8 内装箱，并使用此方法和一个指示本机/语言指针的类型创建。 

[CreateMetadataStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-createmetadatastore)

CreateMetadataStore 方法创建密钥存储，即密钥/值/元组的简化容器，用于保存可与属性关联的元数据和其他各种值。 元数据存储区可能有单个父代（又可以有单个父项）。 如果给定的元数据密钥不在给定的存储中，则检查其父项。 大多数元数据存储没有父级。 不过，它确实提供了一种轻松共享公共元数据的方法。 

[CreateTypedIntrinsicObjectEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager2-createtypedintrinsicobjectex)

CreateTypedIntrinsicObjectEx 方法在语义上类似于 CreateTypedIntrinsicObject 方法。 两者之间唯一的区别在于，此方法允许调用方指定内部数据有效的上下文。 如果未传递任何上下文，则数据在从类型参数继承的任何上下文中都被视为有效（CreateTypedIntrinsicObject 的行为方式）。 这允许在调试目标中创建类型化的指针值，这需要比从类型继承更具体的上下文。 

**扩展性/注册方法**以下一组方法管理数据模型的扩展性机制，使客户端能够扩展或注册现有模型，或要求数据模型在与给定条件匹配的本机类型上自动附加给定的父模型。

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

GetModelForTypeSignature 方法返回通过以前对 RegisterModelForTypeSignature 方法的调用向特定类型签名注册的数据模型。 此方法返回的数据模型被视为与传递的类型签名匹配的任何类型的规范可视化工具。 作为规范化的可视化工具，该数据模型将接管该类型的显示。 默认情况下，显示引擎将隐藏对象的本机/语言构造，以便于数据模型提供的对象的视图。 


[GetModelForType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getmodelfortype)

GetModelForType 方法返回作为给定类型实例的规范可视化工具的数据模型。 实际上，此方法将查找在先前调用 RegisterModelForTypeSignature 方法时注册的最佳匹配类型签名，并返回关联的数据模型。 

[RegisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-registermodelfortypesignature)

RegisterModelForTypeSignature 方法是调用方用来注册给定类型（或类型集）的规范可视化工具的主要方法。 规范化可视化工具是一种数据模型，它实际上会接管给定类型（或类型集）的显示。 显示已注册的数据模型提供的类型的视图，而不是在任何调试器用户界面中显示的类型的本机/语言视图（以及返回到需要该类型的用户的本机/语言视图的方法）。 

[UnregisterModelForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregistermodelfortypesignature)

UnregisterModelForTypeSignature 方法撤消之前对 RegisterModelForTypeSignature 方法的调用。 此方法可以删除给定数据模型作为与特定类型签名匹配的类型的规范可视化工具，也可以删除给定数据模型，作为在其下注册该数据模型的每个类型签名的规范可视化工具。 

[RegisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-registerextensionfortypesignature)

RegisterExtensionForTypeSignature 方法类似于 RegisterModelForTypeSignature 方法，但有一个重要区别。 传递给此方法的数据模型不是任何类型的规范可视化工具，它不会接管该类型的本机/语言视图的显示。 传递给此方法的数据模型将自动添加为与所提供的类型签名匹配的任何具体类型的父级。 与 RegisterModelForTypeSignature 方法不同，被注册为给定类型（或类型集）的扩展的相同或不明确的类型签名没有限制。 类型签名与给定具体类型实例相匹配的每个扩展将导致通过此方法注册的数据模型自动附加到作为父模型的新创建对象。 实际上，这允许任意数量的客户端使用新字段或功能扩展一种类型（或一组类型）。 

[UnregisterExtensionForTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisterextensionfortypesignature)

UnregisterExtensionForTypeSignature 方法撤消之前对 RegisterExtensionForTypeSignature 的调用。 它将特定的数据模型取消注册为特定类型签名的扩展，或取消注册数据模型所针对的所有类型签名的扩展。 

[GetRootNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

GetRootNamespace 方法返回数据模型的根命名空间。 这是数据模型管理的对象，调试宿主将在其中放置某些对象。 

[RegisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-getrootnamespace)

RegisterNamedModel 方法在众所周知的名称下注册给定的数据模型，以便客户端可以找到它。 这是 API 的主要用途-将数据模型发布为可通过检索在此众所周知的名称下注册的模型并向其添加父模型来扩展的内容。 

[UnregisterNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-unregisternamedmodel)

UnregisterNamedModel 方法撤消之前对 RegisterNamedModel 的调用。 它删除了数据模型与可在其中进行查找的名称之间的关联。 

[AcquireNamedModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager-acquirenamedmodel)

如果调用方想要扩展在给定名称下注册的数据模型，则会调用 AcquireNamedModel 方法，以检索要扩展的数据模型的对象。 此方法将返回通过以前对 RegisterNamedModel 方法的调用注册的任何数据模型。 作为 AcquireNamedModel 方法的主要目的是扩展模型，如果尚未在给定名称下注册任何模型，则此方法具有特殊行为。 如果尚未在给定名称下注册任何模型，则将创建一个存根对象，并在给定的名称下临时注册该对象，并将其返回给调用方。 当通过调用 RegisterNamedModel 方法来注册真实数据模型时，对存根对象所做的任何更改实际上是对实际模型进行的任何更改。 这将从互相扩展的组件中删除许多加载顺序依赖关系问题。 


**Helper 方法**

以下方法是常规 helper 方法，有助于对数据模型中的对象执行复杂的操作。 虽然可以通过其他方法对数据模型或其对象执行这些操作，但这些便利方法会使其变得更加容易： 

```cpp
STDMETHOD(AcquireSubNamespace)(_In_ PCWSTR modelName, _In_ PCWSTR subNamespaceModelName, _In_ PCWSTR accessName, _In_opt_ IKeyStore *metadata, _COM_Outptr_ IModelObject **namespaceModelObject) PURE;
```

[AcquireSubNamespace](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelmanager2-acquiresubnamespace)

AcquireSubNamespace 方法有助于构造一些类似于动态语言中的新对象的语言命名空间。 例如，如果调用方想要对进程对象的属性进行分类，使进程对象更井然有序并且属性更易于发现，则执行此操作的一种方法是为 process 对象上的每个类别创建一个子对象，然后将该对象中的这些属性。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

本主题是一系列文章的一部分，其中描述了可C++从访问的接口，如何使用它们C++来生成基于的调试器扩展，以及如何使用其他数据模型构造（例如：JavaScript 或 NatVis） C++ 。

[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++附加接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)

[调试器数据模型C++脚本](data-model-cpp-scripting.md)
