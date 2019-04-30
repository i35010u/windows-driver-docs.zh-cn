---
title: 调试器数据模型 C++ 的概念
description: 本主题介绍在调试器中的概念C++数据模型。
ms.date: 10/04/2018
ms.openlocfilehash: f29334ea8b034f05000b97d2a232ec5c0a250503
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376118"
---
# <a name="debugger-data-model-c-concepts"></a>调试器数据模型 C++ 的概念

本主题介绍在调试器中的概念C++数据模型。

本主题是一系列用于描述可从访问接口的一部分C++，如何使用它们来生成C++调试器扩展，以及如何使基于使用的数据模型的其他构造 (例如：JavaScript 或 NatVis） 从C++数据模型扩展。


[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++对象](data-model-cpp-objects.md)

[调试器数据模型C++的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)

[调试器数据模型C++脚本](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>主题部分

本主题包含以下部分：

[中的数据模型的概念](#concepts) 

---


## <a name="span-idconcepts-concepts-in-the-data-model"></a><span id="concepts"> 中的数据模型的概念 

数据模型中的综合对象是有效地两件事： 

- 元数据键/值元组的字典。
- 支持的数据模型的概念 （接口） 的一组。
概念是提供一组指定的语义行为 （而不是数据模型中） 的客户端实现的接口。 此处列出了当前支持的概念集。 

概念接口 | 描述
|-----------------|-------------|
IDataModelConcept | 这一概念是一个父模型。 如果此模型会自动附加到通过已注册的类型签名的本机类型，InitializeObject 方法将自动调用每次实例化此类类型的新对象。
IStringDisplayableConcept | 对象可以转换为用于显示目的的字符串。
IIterableConcept | 对象是一个容器，并且可以循环访问。
IIndexableConcept | 该对象是一个容器，并且可以进行索引 （通过随机访问访问） 中一个或多个维度。
IPreferredRuntimeTypeConcept | 该对象了解有关派生自它不是基础类型系统能够提供，并且想要处理其自身从静态到运行时类型的转换的类型的详细信息。
IDynamicKeyProviderConcept | 对象是动态的提供程序的密钥，并且想要接管的核心数据模型中的所有键查询。 此接口通常用作与 JavaScript 等动态语言的桥梁。
IDynamicConceptProviderConcept | 对象是动态的提供程序的概念，并且想要接管的核心数据模型中的所有概念查询。 此接口通常用作与 JavaScript 等动态语言的桥梁。


**数据模型概念：IDataModelConcept**

任何模型对象附加到另一个模型对象，作为父模型必须直接支持的数据模型概念。 数据模型概念需要支持接口、 IDataModelConcept 定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDataModelConcept, IUnknown)
{
    STDMETHOD(InitializeObject)(_In_ IModelObject* modelObject, _In_opt_ IDebugHostTypeSignature* matchingTypeSignature, _In_opt_ IDebugHostSymbolEnumerator* wildcardMatches) PURE;
    STDMETHOD(GetName)(_Out_ BSTR* modelName) PURE;
}
```

[InitializeObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelconcept-initializeobject)

可以通过数据模型管理器的 RegisterModelForTypeSignature 或 RegisterExtensionForTypeSignature 方法中注册为规范的可视化工具或给定的本机类型的扩展数据模型。 通过其中一种方法注册一个模型时，数据模型会自动附加作为父模型为其类型与注册中传递的签名匹配的任何本机对象。 会自动成为该附件的点，在数据模型上调用 InitializeObject 方法。 传递的实例对象、 类型签名会导致附件和它将生成 （按线性顺序） 的匹配类型签名中的任何通配符的类型实例的枚举器。 数据模型实现可能使用此方法调用来初始化它要求任何缓存。 

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelconcept-getname)

如果通过 RegisterNamedModel 方法的默认名称注册为给定的数据模型时，已注册的数据模型的 IDataModelConcept 接口必须从此方法返回该名称。 请注意，若要在其下多个名称 （默认值或一个应在此处返回的最佳） 注册为模型完全合法。 （只要它未注册名称下），模型可能会完全未命名。 在这种情况下，GetName 方法应返回 E_NOTIMPL。 


**字符串可显示概念：IStringDisplayableConcept**

想要提供用于显示的字符串转换的对象可以实现通过 IStringDisplayableConcept 接口的实现的字符串可显示概念。 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IStringDisplayableConcept, IUnknown)
{
    STDMETHOD(ToDisplayString)(_In_ IModelObject* contextObject, _In_opt_ IKeyStore* metadata, _Out_ BSTR* displayString) PURE;
}
```

[ToDisplayString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-istringdisplayableconcept-todisplaystring)

每当客户端想要将对象转换为字符串，用于显示调用 ToDisplayString 方法 (若要在 UI 中，控制台等...)。此类字符串转换不应该用于其他编程操作的基础。 字符串转换本身可能深度受传递给调用的元数据。 字符串转换应使每次尝试遵循的 PreferredRadix 和 PreferredFormat 键。 


**可迭代的概念：IIterableConcept 和 IModelIterator**

这是其他对象的容器，并且想要快速循环访问这些包含对象的功能的对象可以通过 IIterableConcept 和 IModelIterator 接口的实现支持可迭代的概念。 没有可迭代的概念的支持和支持可编制索引的概念之间的非常重要的关系。 支持对包含的对象的随机访问的对象可以支持除了可迭代的概念可编制索引的概念。 在这种情况下，循环访问的元素也必须生成默认值编制索引，传递给可编制索引的概念时引用同一对象。 未能满足这个固定条件将导致调试主机中未定义的行为。 

IIterableConcept 定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IIterableConcept, IUnknown)
{
    STDMETHOD(GetDefaultIndexDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetIterator)(_In_ IModelObject* contextObject, _Out_ IModelIterator** iterator) PURE;
}
```

IModelIterator 概念的定义如下： 

```cpp
DECLARE_INTERFACE_(IModelIterator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Errorptr_ IModelObject** object, _In_ ULONG64 dimensions, _Out_writes_opt_(dimensions) IModelObject** indexers, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

IIterableConcept 的[GetDefaultIndexDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iiterableconcept-getdefaultindexdimensionality)

GetDefaultIndexDimensionality 方法返回到默认索引的维度数。 如果对象不是可编制索引，此方法应返回 0，成功 (S_OK)。 这将从此方法返回一个非零值的任何对象声明对状态的协议协定的支持： 
- 对象支持通过 IIndexableConcept 支持可编制索引的概念
- 从可迭代概念 GetIterator 方法返回 IModelIterator GetNext 方法将返回生成的每个元素的唯一默认索引。 此处所示，这样的索引将具有维度的数目。
- 传递从 IModelIterator GetNext 方法返回到 GetAt 方法，可编制索引的概念上索引 (IIndexableConcept) 将引用 GetNext 生成的相同对象。 返回相同的值。

IIterableConcept 的[GetIterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iiterableconcept-getiterator)

可迭代的概念的 GetIterator 方法返回可用于循环访问该对象的迭代器接口。 返回迭代器必须记住已传递给 GetIterator 方法的上下文对象。 它不会传递到对自身的迭代器方法。 


IModelIterator 的[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodeliterator-reset)

返回从可迭代的概念的迭代器上的重置方法将迭代器的位置还原至时的状态 （在之前的第一个元素） 首次创建迭代器。 虽然强烈建议该迭代器的支持重置方法，也不需要。 一个迭代器，可以是等效的C++输入迭代器，仅允许向前迭代一次传递。 在这种情况下，重置方法可能会因 E_NOTIMPL。 

IModelIterator 的[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-imodeliterator-getnext)

GetNext 方法向前移动迭代器，并提取下一个循环访问的元素。 如果对象是除了可迭代可编制索引，这会由 GetDefaultIndexDimensionality 参数返回一个非零值指示，此方法可能会根据需要返回默认索引以返回到生成的值从索引器。 请注意，调用方可能选择传递 0/nullptr 和检索任何索引。 它被认为是非法的调用方请求部分索引 (例如： 小于 GetDefaultIndexDimensionality 生成数)。 

如果迭代器向前移动成功，但在读取循环访问元素的值时出错，该方法可能返回错误*AND*填充"对象"的错误对象。 在所含元素的迭代结束时，迭代器将从 GetNext 方法返回 E_BOUNDS。 任何后续调用 （除非已进行干预调用重置） 也将返回 E_BOUNDS。 


**可编制索引的概念：IIndexableConcept**

想要提供对内容集的随机访问的对象可以支持通过支持 IIndexableConcept 接口可编制索引的概念。 为可编制索引的大多数对象将可迭代以及通过支持的可迭代的概念。 这不是，但是，必需。 如果支持，则迭代器和索引器之间的重要关系。 迭代器必须支持 GetDefaultIndexDimensionality、 从该方法返回一个非零值和支持协定那里记录。 索引器概念接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IIndexableConcept, IUnknown)
{
    STDMETHOD(GetDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _COM_Errorptr_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _In_ IModelObject *value) PURE;
}
```

使用索引器 （和其交互作用于迭代器） 的示例如下所示。 此示例循环访问可编制索引的容器的内容，并使用索引器以返回到刚返回的值。 功能上无用写入该操作时，它演示了这些接口的交互方式。 请注意，下面的示例不应对内存分配失败。 它假定引发新 (这可能会根据环境中存在代码--数据模型的 COM 方法不能有一个不佳假设C++异常转义): 

```cpp
ComPtr<IModelObject> spObject;

//
// Assume we have gotten some object in spObject that is iterable (e.g.: an object which represents a std::vector<SOMESTRUCT>)
//
ComPtr<IIterableConcept> spIterable;
ComPtr<IIndexableConcept> spIndexer;
if (SUCCEEDED(spObject->GetConcept(__uuidof(IIterableConcept), &spIterable, nullptr)) &&
    SUCCEEDED(spObject->GetConcept(__uuidof(IIndexableConcept), &spIndexable, nullptr)))
{
    ComPtr<IModelIterator> spIterator;

    //
    // Determine how many dimensions the default indexer is and allocate the requisite buffer.
    //
    ULONG64 dimensions;
    if (SUCCEEDED(spIterable->GetDefaultIndexDimensionality(spObject.Get(), &dimensions)) && dimensions > 0 &&
        SUCCEEDED(spIterable->GetIterator(spObject.Get(), &spIterator)))
    {
        std::unique_ptr<ComPtr<IModelObject>[]> spIndexers(new ComPtr<IModelObject>[dimensions]);

        //
        // We have an iterator.  Error codes have semantic meaning here.  E_BOUNDS indicates the end of iteration.  E_ABORT indicates that
        // the debugger host or application is trying to abort whatever operation is occurring.  Anything else indicates
        // some other error (e.g.: memory read failure) where the iterator MIGHT still produce values.
        //
        for(;;)
        {
            ComPtr<IModelObject> spContainedStruct;
            ComPtr<IKeyStore> spContainedMetadata;

            //
            // When we fetch the value from the iterator, it will pass back the default indicies.
            //
            HRESULT hr = spIterable->GetNext(&spContainedStruct, dimensions, reinterpret_cast<IModelObject **>(spIndexers.get()), &spContainedMetadata);
            if (hr == E_BOUNDS || hr == E_ABORT)
            {
                break;
            }

            if (FAILED(hr))
            {
                //
                // Decide how to deal with failure to fetch an element.  Note that spContainedStruct *MAY* contain an error object
                // which has detailed information about why the failure occurred (e.g.: failure to read memory at address X).
                //
            }

            //
            // Use the indexer to get back to the same value.  We already have them, so there isn't much functional point to this.  It simply
            // highlights the interplay between iterator and indexer.
            //
            ComPtr<IModelObject> spIndexedStruct;
            ComPtr<IKeyStore> spIndexedMetadata;

            if (SUCCEEDED(spIndexer->GetAt(spObject.Get(), dimensions, reinterpret_cast<IModelObject **>(spIndexers.get()), &spIndexedStruct, &spIndexedMetadata)))
            {
                //
                // spContainedStruct and spIndexedStruct refer to the same object.  They may not have interface equality.
                // spContainedMetadata and spIndexedMetadata refer to the same metadata store with the same contents.  They may not have interface equality.
                //
            }
        }
    }
}
```


[GetDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-getdimensionality)

GetDimensionality 方法返回对象进行索引中的维度的数。 注意如果对象是可迭代并可编制索引，GetDefaultIndexDimensionality 的实现必须同意有关多少维度索引器 GetDimensionality 实现具有。 

[GetAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-getat)

GetAt 方法检索从索引对象中的特定 N 维索引处的值。 必须支持 N 维度其中 N 是从 GetDimensionality 返回的值的索引器。 请注意，对象可能是可索引由不同类型的不同域中 (例如： 通过序号和字符串可编制索引)。 如果索引超出范围 （或无法访问），该方法将返回故障;但是，在这种情况下，输出对象可能仍设置为一个错误对象。 

[SetAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-iindexableconcept-setat)

SetAt 方法尝试将值设置在从索引对象中的特定 N 维索引。 必须支持 N 维度其中 N 是从 GetDimensionality 返回的值的索引器。 请注意，对象可能是可索引由不同类型的不同域中 (例如： 通过序号和字符串可编制索引)。 某些索引器是只读的。 在这种情况下，将任何调用与 SetAt 方法调用返回 E_NOTIMPL。 


**首选的运行时类型概念：IPreferredRuntimeTypeConcept**

调试主机可以通过查询来尝试确定真正的运行时类型的符号化信息中找到的静态类型中的对象。 此转换可能基于完全准确的信息 (例如：C++RTTI) 也可能基于强启发式方法，如在对象中的任何虚拟函数表的形状。 某些对象，但是，不能将从转换静态运行时类型因为它们不适合于调试主机的试探法 (例如： 它们不具有 RTTI 或虚函数表)。 在这种情况下，对象的数据模型可以选择重写默认行为，并声明，它才知道更多对象的"运行时类型"不是它能够了解调试主机。 这是通过首选的运行时类型概念和 IPreferredRuntimeTypeConcept 接口的支持。 

IPreferredRuntimeTypeConcept 接口声明，如下所示： 

```cpp
DECLARE_INTERFACE_(IPreferredRuntimeTypeConcept, IUnknown)
{
    STDMETHOD(CastToPreferredRuntimeType)(_In_ IModelObject* contextObject, _COM_Errorptr_ IModelObject** object) PURE;
}
```

[CastToPreferredRuntimeType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ipreferredruntimetypeconcept-casttopreferredruntimetype)

只要客户端想要尝试从静态类型实例转换为该实例的运行时类型，则会调用 CastToPreferredRuntimeType 方法。 如果相关对象 （通过一个及其附加的父模型） 支持首选的运行时类型概念，将调用此方法来执行此转换。 此方法可能会返回原始对象 （不存在转换或未能分析），则返回的运行时类型的新实例，非语义的原因而失败 (例如： 内存不足)，或返回 E_NOT_SET。 E_NOT_SET 错误代码是一个非常特殊的错误代码，它表示到数据模型的实现不想重写默认行为和数据模型应回退到任何分析由调试主机 （例如执行:RTTI 分析、 检查形状的虚函数表，等等。...) 


**动态提供程序的概念：IDynamicKeyProviderConcept 和 IDynamicConceptProviderConcept**

虽然数据的模型本身通常为对象的句柄密钥和概念管理，有些时候这种观点是不太理想。 具体而言，当客户端想要创建数据模型和其他内容之间的桥梁，这是真正的动态 (例如：JavaScript)，它可以是有价值以接管密钥和概念数据模型中的实现。 由于核心数据模型是一个，实现 IModelObject，而这是通过组合两个概念： 动态密钥提供程序和动态的概念提供程序概念。 尽管有的典型实现这两个还是两者皆否，没有任何要求对这些产品。 

如果同时实现了，动态密钥提供程序概念之前，必须添加动态的概念提供程序概念。 这些概念都特殊。 它们有效地将它从"静态托管"更改为"动态托管"的对象上翻转开关。 如果管理的对象上的数据模型没有密钥/概念，可以仅设置这些概念。 这些概念添加到一个对象后, 执行此操作的操作是不可撤消。 

其他语义之间没有区别围绕扩展性 IModelObject 这是动态的概念提供程序和一个则没有。 这些概念被为了让客户端以创建数据模型和 JavaScript 等动态语言系统之间的桥梁。 数据模型具有一个概念，因为树的父模型而不是像 JavaScript 原型链的线性链，某种程度上从根本上不同于 JavaScript 等系统实现的扩展性。 若要允许对此类系统更加融洽的关系，这是动态的概念提供程序 IModelObject 具有单个数据模型父级。 该单个数据模型父级就是正常 IModelObject 可具有任意数目的父模型如是典型的数据模型。 对要添加或删除父项的动态的概念提供程序的任何请求会自动重定向到单一父中。 从外部人员的角度来看，它看起来像动态的概念提供程序具有的父模型正常树样式链。 动态的概念提供程序概念的实施者是可以识别的中间单个父 （之外的核心数据模型） 的唯一对象。 可以对动态语言系统提供桥链接该单一父 (例如： 放入 JavaScript 原型链)。 

动态密钥提供程序概念定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDynamicKeyProviderConcept, IUnknown)
{
    STDMETHOD(GetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _COM_Outptr_opt_result_maybenull_ IModelObject** keyValue, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata, _Out_opt_ bool *hasKey) PURE;
    STDMETHOD(SetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _In_ IModelObject *keyValue, _In_ IKeyStore *metadata) PURE;
    STDMETHOD(EnumerateKeys)(_In_ IModelObject *contextObject, _COM_Outptr_ IKeyEnumerator **ppEnumerator) PURE;
}
```

动态的概念提供程序概念定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDynamicConceptProviderConcept, IUnknown)
{
    STDMETHOD(GetConcept)(_In_ IModelObject *contextObject, _In_ REFIID conceptId, _COM_Outptr_result_maybenull_ IUnknown **conceptInterface, _COM_Outptr_opt_result_maybenull_ IKeyStore **conceptMetadata, _Out_ bool *hasConcept) PURE;
    STDMETHOD(SetConcept)(_In_ IModelObject *contextObject, _In_ REFIID conceptId, _In_ IUnknown *conceptInterface, _In_opt_ IKeyStore *conceptMetadata) PURE;
    STDMETHOD(NotifyParent)(_In_ IModelObject *parentModel) PURE;
    STDMETHOD(NotifyParentChange)(_In_ IModelObject *parentModel) PURE;
    STDMETHOD(NotifyDestruct)() PURE;
}
```

IDynamicKeyProviderConcept's [GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-getkey)

动态密钥提供程序上的 GetKey 方法是很大程度上 IModelObject GetKey 方法的重写。 动态密钥提供程序应返回的值的密钥和使用该密钥相关联的任何元数据。 如果该键不存在 （但会发生任何其他错误），该提供程序必须返回 false hasKey 参数中，并成功使用，则为 S_OK。 失败的此调用被认为是失败来提取密钥和显式停止搜索通过父模型链密钥。 返回 false hasKey 和成功中将继续执行搜索的密钥。 请注意，完全合法的 GetKey 返回装箱的属性访问器作为键。 这将是 GetKey 方法 IModelObject 返回属性访问器在语义上完全相同。 

IDynamicKeyProviderConcept's [SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-setkey)

动态密钥提供程序上的 setkey 权限方法实际上是 IModelObject 的 setkey 权限方法的重写。 此动态提供程序中设置的密钥。 它实际上是属性的创建新的提供程序。 请注意不支持任何概念类似于 expando 属性创建的提供程序应返回 E_NOTIMPL 此处。 

IDynamicKeyProviderConcept 的[EnumerateKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-enumeratekeys)

动态密钥提供程序上的 EnumerateKeys 方法实际上是 IModelObject EnumerateKeys 方法的重写。 此枚举中动态提供程序的所有键。 返回的枚举数具有多个实现必须遵循的限制： 

- 它必须用作对 EnumerateKeys 不 EnumerateKeyValues 或 EnumerateKeyReferences 的调用。 它必须返回不解决任何基础属性访问器 （如果提供程序中存在此类概念） 的注册表项值。
- 从单一的动态密钥提供程序的角度来看，您不能枚举多个具有相同名称的键，它们都以物理方式非重复键。 在不同的父模型链，通过附加的提供程序上发生这种情况，但它不能从单个提供程序的角度来看发生这种情况。

IDynamicConceptProviderConcept's [GetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-getconcept)

动态的概念提供程序上的 GetConcept 方法实际上是 IModelObject GetConcept 方法的重写。 如果存在与此概念相关联的任何元数据以及动态的概念提供程序必须返回一个接口，使查询的概念。 如果必须通过 hasConcept 参数和一个成功的返回语句中返回的值为 false 指示的提供程序上不存在这一概念。 此方法的故障故障来提取这一概念，并且将显式暂停搜索这一概念。 返回 false hasConcept 和成功的代码将继续搜索的父模型树的概念。 

IDynamicConceptProviderConcept's [SetConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-setconcept)

动态的概念提供程序上的 SetConcept 方法实际上是 IModelObject SetConcept 方法的重写。 动态提供程序将分配这一概念。 这可能会导致对象可迭代、 可编制索引，字符串转换，等等...请注意不允许对其进行概念创建的提供程序应返回 E_NOPTIMPL 此处。 

IDynamicConceptProviderConcept's [NotifyParent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparent)

核心数据模型使用动态的概念提供程序上 NotifyParent 调用以通知动态创建桥接到更加动态语言的数据模型的"多个父模型"模式允许的单一父模型的提供程序。 该单个父模型的任何操作将会产生其他通知到动态提供程序。 请注意，此回调动态的概念提供程序概念的分配时立即进行。 

IDynamicConceptProviderConcept's [NotifyParentChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparentchange)

动态的概念提供程序上的 NotifyParent 方法是进行静态对象的单个父模型的操作时所做的核心数据模型的回调。 对于任何给定的父模型中添加，此方法将调用时所述的父模型已添加和删除父模型第二次时所说的第一次。 

IDynamicConceptProviderConcept's [NotifyDestruct](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifydestruct)

动态的概念提供程序上的 NotifyDestruct 方法为回调所做的是动态的概念提供程序的对象的析构开头的核心数据模型。 它会向客户端需要它提供更多清理的机会。 


---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++对象](data-model-cpp-objects.md)

[调试器数据模型C++的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)

[调试器数据模型C++脚本](data-model-cpp-scripting.md)


 

 






