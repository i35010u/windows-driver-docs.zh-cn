---
title: 调试器数据模型 C++ 的概念
description: 本主题介绍调试器 c + + 数据模型中的概念。
ms.date: 09/12/2019
ms.openlocfilehash: 4814bc038c6dacc3c7f10c1f6d911e8dd3164544
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209875"
---
# <a name="debugger-data-model-c-concepts"></a>调试器数据模型 C++ 的概念

本主题介绍调试器 c + + 数据模型中的概念。

## <a name="span-idconcepts-concepts-in-the-data-model"></a><span id="concepts"> 数据模型中的概念 

数据模型中的综合对象实际上有两个用途： 

- 键/值/元组的字典。
- 数据模型支持的 (接口) 的一组概念。
概念是指客户端 (的接口，而不是数据模型) 实现以提供一组指定的语义行为。 此处列出了当前支持的概念集。 

概念接口 | 说明
|-----------------|-------------|
IDataModelConcept | 概念是一个父模型。 如果通过注册的类型签名将此模型自动附加到本机类型，则每次实例化此类类型的新对象时，都会自动调用 InitializeObject 方法。
IStringDisplayableConcept | 出于显示目的，可以将对象转换为字符串。
IIterableConcept | 对象是一个容器，可以循环访问。
IIndexableConcept | 对象是一个容器，可以通过在一个或多个维度中通过随机访问) 进行索引 (访问。
IPreferredRuntimeTypeConcept | 对象更详细地了解派生自它的类型，而不是基础类型系统能够提供，并希望处理其自己的从静态到运行时类型的转换。
IDynamicKeyProviderConcept | 对象是密钥的动态提供程序，希望接管核心数据模型中的所有关键查询。 此接口通常用作动态语言（如 JavaScript）的桥。
IDynamicConceptProviderConcept | 对象是概念的动态提供程序，希望接管核心数据模型中的所有概念查询。 此接口通常用作动态语言（如 JavaScript）的桥。


**数据模型概念： IDataModelConcept**

附加到作为父模型的另一个模型对象的任何模型对象必须直接支持数据模型概念。 数据模型概念需要接口，IDataModelConcept 的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelConcept, IUnknown)
{
    STDMETHOD(InitializeObject)(_In_ IModelObject* modelObject, _In_opt_ IDebugHostTypeSignature* matchingTypeSignature, _In_opt_ IDebugHostSymbolEnumerator* wildcardMatches) PURE;
    STDMETHOD(GetName)(_Out_ BSTR* modelName) PURE;
}
```

[InitializeObject](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelconcept-initializeobject)

通过数据模型管理器的 RegisterModelForTypeSignature 或 RegisterExtensionForTypeSignature 方法，可以将数据模型注册为规范化可视化工具或给定本机类型的扩展。 当通过这两种方法之一注册模型时，数据模型会自动作为父模型附加到其类型与注册中传递的签名相匹配的任何本机对象。 在自动执行该附件的位置，将对数据模型调用 InitializeObject 方法。 它被传递给实例对象、导致附件的类型签名，以及生成类型实例的枚举器，该枚举器 (以线性顺序) 匹配类型签名中的任何通配符。 数据模型实现可以使用此方法调用来初始化它所需的任何缓存。 

[GetName](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelconcept-getname)

如果给定数据模型通过 RegisterNamedModel 方法在默认名称下注册，则已注册的数据模型的 IDataModelConcept 接口必须从此方法返回该名称。 请注意，对于使用多个名称注册的模型而言，它是完全合法的， (应在此处) 返回默认值或最佳名称。 只要模型未在名称) 下注册，就可以完全命名 (。 在这种情况下，GetName 方法应返回 E_NOTIMPL。 


**字符串可显示概念： IStringDisplayableConcept**

希望为显示目的提供字符串转换的对象可通过实现 IStringDisplayableConcept 接口实现字符串可显示概念。 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IStringDisplayableConcept, IUnknown)
{
    STDMETHOD(ToDisplayString)(_In_ IModelObject* contextObject, _In_opt_ IKeyStore* metadata, _Out_ BSTR* displayString) PURE;
}
```

[ToDisplayString](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-istringdisplayableconcept-todisplaystring)

每当客户端希望将对象转换为字符串，以便在用户界面中 (显示控制台时，就会调用 ToDisplayString 方法。) 。此类字符串转换不应用于其他编程操作的基础。 字符串转换本身可能会受到传递到调用的元数据的深度影响。 字符串转换应每次尝试服从 PreferredRadix 和 PreferredFormat 键。 


**可迭代概念： IIterableConcept 和 IModelIterator**

一个对象，它是其他对象的容器，希望能够循环访问所包含的对象，从而能够通过实现 IIterableConcept 和 IModelIterator 接口来支持可迭代概念。 支持可迭代概念与可编制索引的概念之间存在一个非常重要的关系。 支持对所包含的对象进行随机访问的对象可以支持可索引的概念以及可迭代的概念。 在这种情况下，迭代的元素还必须生成默认索引，在将其传递给可索引的概念时，请引用相同的对象。 未能满足此固定条件将导致调试宿主中出现未定义的行为。 

IIterableConcept 定义如下： 

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

IIterableConcept 的 [GetDefaultIndexDimensionality](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-iiterableconcept-getdefaultindexdimensionality)

GetDefaultIndexDimensionality 方法将维度数返回给默认索引。 如果对象不可建立索引，此方法应返回0并成功 (S_OK) 。 从此方法返回非零值的任何对象都是声明对协议协定的支持，该协定指出： 
- 对象通过支持 IIndexableConcept 支持可索引的概念
- 从可迭代概念的 GetIterator 方法返回的 IModelIterator 的 GetNext 方法将为每个生成的元素返回唯一的默认索引。 此类索引将具有如下所示的维度数。
- 将从 IModelIterator 的 GetNext 方法返回的索引传递到可编制索引的概念上的 GetAt 方法 (IIndexableConcept) 将引用 GetNext 生成的同一对象。 返回相同的值。

IIterableConcept 的 [GetIterator](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-iiterableconcept-getiterator)

可迭代概念上的 GetIterator 方法返回一个迭代器接口，该接口可用于循环访问对象。 返回的迭代器必须记住传递到 GetIterator 方法的上下文对象。 它不会传递给迭代器本身上的方法。 


IModelIterator 的 [重置](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodeliterator-reset)

从可迭代概念返回的迭代器上的 Reset 方法会将迭代器的位置还原到首次创建迭代器的位置 (第一个元素) 之前。 尽管强烈建议迭代器支持 Reset 方法，但这并不是必需的。 迭代器可以是 c + + 输入迭代器的等效项，只允许一轮向前迭代。 在这种情况下，Reset 方法可能会失败，并 E_NOTIMPL。 

IModelIterator 的 [GetNext](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-imodeliterator-getnext)

GetNext 方法向前移动迭代器并提取下一个迭代的元素。 如果对象是可索引的（除了可迭代），并且 GetDefaultIndexDimensionality 参数指示返回非零值，则此方法可能会选择返回默认索引，以返回到索引器中的生成值。 请注意，调用方可以选择传递 0/nullptr，而不检索任何索引。 对于调用方，请求部分索引 (（例如：小于 GetDefaultIndexDimensionality) 生成的数目），这是非法的。 

如果迭代器成功地向前移动，但在读取循环访问的元素的值时出错，则该方法可能返回错误 *并* 使用错误对象填充 "对象"。 在包含的元素迭代结束时，迭代器将从 GetNext 方法返回 E_BOUNDS。 任何后续调用 (除非发生了介入的重置呼叫) 也会返回 E_BOUNDS。 


**可编制索引的概念： IIndexableConcept**

希望提供对一组内容的随机访问的对象，可通过支持 IIndexableConcept 接口支持可索引的概念。 大多数可编制索引的对象也会通过支持可迭代概念进行可迭代。 但这并不是必需的。 如果支持，迭代器与索引器之间存在重要的关系。 迭代器必须支持 GetDefaultIndexDimensionality，并从该方法返回一个非零值，并支持在此方法中记录的协定。 索引器概念接口定义如下： 

```cpp
DECLARE_INTERFACE_(IIndexableConcept, IUnknown)
{
    STDMETHOD(GetDimensionality)(_In_ IModelObject* contextObject, _Out_ ULONG64* dimensionality) PURE;
    STDMETHOD(GetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _COM_Errorptr_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(SetAt)(_In_ IModelObject* contextObject, _In_ ULONG64 indexerCount, _In_reads_(indexerCount) IModelObject** indexers, _In_ IModelObject *value) PURE;
}
```

下面显示了使用索引器 (及其相互作用与迭代器) 的示例。 此示例将循环访问可索引容器的内容，并使用索引器返回到刚返回的值。 尽管该操作在功能上是不能编写的，但它演示了这些接口如何交互。 请注意，下面的示例不处理内存分配失败。 它假定引发新的 (这可能是一种不好的假设，具体取决于代码所在的环境，数据模型的 COM 方法不能有 c + + 异常转义) ： 

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


[GetDimensionality](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-iindexableconcept-getdimensionality)

GetDimensionality 方法返回在其中对对象进行索引的维度数。 请注意，如果对象既是可迭代又是可编制索引的，则 GetDefaultIndexDimensionality 的实现必须与索引器的实现方式一致。 

[GetAt](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-iindexableconcept-getat)

GetAt 方法检索索引对象中特定 N 维索引处的值。 N 维的索引器，其中 N 是从 GetDimensionality 返回的值必须受支持。 请注意，不同类型的对象可以在不同的域中建立索引 (例如：可通过序号和字符串) 进行索引。 如果索引超出范围 (或无法) 访问，则方法将返回失败;但是，在这种情况下，输出对象可能仍设置为错误对象。 

[SetAt](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-iindexableconcept-setat)

SetAt 方法尝试在索引对象中设置特定 N 维索引处的值。 N 维的索引器，其中 N 是从 GetDimensionality 返回的值必须受支持。 请注意，不同类型的对象可以在不同的域中建立索引 (例如：可通过序号和字符串) 进行索引。 某些索引器是只读的。 在这种情况下，将从对 SetAt 方法的任何调用返回 E_NOTIMPL。 


**首选的运行时类型概念： IPreferredRuntimeTypeConcept**

可以查询调试宿主，以尝试从符号信息中找到的静态类型确定对象的实际运行时类型。 这种转换可能基于完全准确的信息 (例如： c + + RTTI) 或基于强试探法，例如对象内任何虚拟函数表的形状。 但是，某些对象无法从静态转换为运行时类型，因为它们不适合调试主机的试探法 (例如：它们没有 RTTI 或虚函数表) 。 在这种情况下，对象的数据模型可选择重写默认行为，并声明它知道对象的 "运行时类型" 比调试宿主能够理解的更多。 这是通过首选的运行时类型概念和对 IPreferredRuntimeTypeConcept 接口的支持来完成的。 

IPreferredRuntimeTypeConcept 接口的声明方式如下： 

```cpp
DECLARE_INTERFACE_(IPreferredRuntimeTypeConcept, IUnknown)
{
    STDMETHOD(CastToPreferredRuntimeType)(_In_ IModelObject* contextObject, _COM_Errorptr_ IModelObject** object) PURE;
}
```

[CastToPreferredRuntimeType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ipreferredruntimetypeconcept-casttopreferredruntimetype)

只要客户端想要尝试从静态类型实例转换为该实例的运行时类型，就会调用 CastToPreferredRuntimeType 方法。 如果相关对象支持 (通过其附加父模型之一) 首选运行时类型概念，则将调用此方法来执行转换。 此方法可能会返回原始对象 (没有转换，或者无法) 分析、返回运行时类型的新实例、因非语义原因而失败， (例如：内存不足) 或返回 E_NOT_SET。 E_NOT_SET 错误代码是一个非常特殊的错误代码，它向数据模型表明，实现不想重写默认行为，而且数据模型应回退到由调试主机执行的任何分析 (例如： RTTI 分析、虚拟函数表的形状检查等。)  


**动态提供程序概念： IDynamicKeyProviderConcept 和 IDynamicConceptProviderConcept**

尽管数据模型本身通常处理对象的关键和概念管理，但在某些情况下，这种概念并不理想。 特别是，当客户端想要在数据模型与其他真正动态 (（例如： JavaScript) ）之间创建桥梁时，从数据模型中的实现接管密钥和概念管理可能是有价值的。 因为核心数据模型是 IModelObject 的唯一实现，所以这是通过两个概念的组合来实现的：动态密钥提供程序的概念和动态概念提供程序的概念。 尽管这两种方法都是典型实现的，但这种情况并不是必需的。 

如果同时实现两者，则必须先添加动态密钥提供程序的概念，然后再添加动态概念提供程序概念。 这两个概念是特殊的。 它们会有效地翻转对象上的开关，使其从 "静态管理" 改为 "动态管理"。 仅当对象上没有由数据模型管理的键/概念时，才能设置这些概念。 将这些概念添加到对象后，执行此操作的操作是不可撤消的。 

在 IModelObject （它是一个动态概念提供程序，另一个不是）之间的扩展性方面有额外的语义差异。 这些概念旨在允许客户端创建数据模型和动态语言系统（如 JavaScript）之间的桥梁。 数据模型具有可扩展性的概念，这一点在本质上不同于 JavaScript，因为有一个父模型树，而不是一个线性链，如 JavaScript 原型链。 为了更好地与此类系统的关系，作为动态概念提供程序的 IModelObject 具有单个数据模型父级。 该单一数据模型父级是一个普通的 IModelObject，它可以具有任意数量的父模型，这与数据模型的典型值相同。 对动态概念提供程序的任何向添加或删除父项发出的请求都将自动重定向到单个父项。 从无形中的角度看，它看起来像动态概念提供程序具有父模型的常规树样式链。 动态概念提供程序概念的实施者是 (核心数据模型外部的唯一对象，) 知道中间单一父级。 单个父代可以与动态语言系统相链接，以提供一个桥 (例如：放入 JavaScript 原型链) 。 

动态密钥提供程序的概念定义如下： 

```cpp
DECLARE_INTERFACE_(IDynamicKeyProviderConcept, IUnknown)
{
    STDMETHOD(GetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _COM_Outptr_opt_result_maybenull_ IModelObject** keyValue, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata, _Out_opt_ bool *hasKey) PURE;
    STDMETHOD(SetKey)(_In_ IModelObject *contextObject, _In_ PCWSTR key, _In_ IModelObject *keyValue, _In_ IKeyStore *metadata) PURE;
    STDMETHOD(EnumerateKeys)(_In_ IModelObject *contextObject, _COM_Outptr_ IKeyEnumerator **ppEnumerator) PURE;
}
```

动态概念提供程序概念定义如下： 

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

IDynamicKeyProviderConcept 的 [GetKey](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-getkey)

动态密钥提供程序的 GetKey 方法主要用于重写 IModelObject 上的 GetKey 方法。 动态密钥提供程序应返回密钥的值以及与该键关联的任何元数据。 如果该键不存在 (但) 不会发生其他错误，则提供程序必须在 hasKey 参数中返回 false，并成功完成 S_OK。 此调用失败将被视为无法获取密钥，并且会通过父模型链显式停止搜索该密钥。 如果在 hasKey 和 success 中返回 false，将继续搜索该密钥。 请注意，GetKey 将已装箱的属性访问器作为键返回是完全合法的。 这在语义上与返回属性访问器的 IModelObject 上的 GetKey 方法相同。 

IDynamicKeyProviderConcept 的 [SetKey](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-setkey)

动态密钥提供程序的 SetKey 方法实际上是对 IModelObject 上的 SetKey 方法的重写。 这会在动态提供程序中设置密钥。 它实际上是在提供程序上创建新属性。 请注意，不支持诸如创建 expando 属性的任何概念的提供程序应在此处返回 E_NOTIMPL。 

IDynamicKeyProviderConcept 的 [EnumerateKeys](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamickeyproviderconcept-enumeratekeys)

动态密钥提供程序的 EnumerateKeys 方法实际上是对 IModelObject 上的 EnumerateKeys 方法的重写。 这会枚举动态提供程序中的所有键。 返回的枚举器具有几个必须由实现实现的限制： 

- 它必须作为对 EnumerateKeys 的调用，而不是 EnumerateKeyValues 或 EnumerateKeyReferences。 如果提供程序) 中存在此类概念，则它必须返回未解析任何基础属性访问器 (的键值。
- 从单个动态密钥提供程序的角度来看，枚举名称与物理上不同的键的多个键是非法的。 这可能发生在通过父模型链附加的不同提供程序上，但不能从单个提供程序的角度进行。

IDynamicConceptProviderConcept 的 [GetConcept](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-getconcept)

动态概念提供程序的 GetConcept 方法实际上是对 IModelObject 上的 GetConcept 方法的重写。 动态概念提供程序必须返回所查询的概念的接口（如果存在）以及与该概念关联的任何元数据。 如果提供程序中不存在该概念，则必须通过在 hasConcept 参数中返回的错误和成功返回值来指示。 此方法失败是无法获取概念的，它会显式停止搜索概念。 如果 hasConcept 返回 false，并且成功的代码将继续通过父模型树搜索概念。 

IDynamicConceptProviderConcept 的 [SetConcept](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-setconcept)

动态概念提供程序的 SetConcept 方法实际上是对 IModelObject 上的 SetConcept 方法的重写。 动态提供程序将分配该概念。 这可能会使对象可迭代、可索引、字符串转换等 .。。请注意，不允许在其上创建概念的提供程序应在此处返回 E_NOPTIMPL。 

IDynamicConceptProviderConcept 的 [NotifyParent](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparent)

动态概念提供程序的 NotifyParent 调用由核心数据模型用来通知单一父模型的动态提供程序，该提供程序创建为允许将数据模型的 "多个父模型" 范例桥接到更多动态语言。 此单个父模型的任何操作都将对动态提供程序产生进一步的通知。 请注意，此回调是在分配动态概念提供程序概念后立即进行的。 

IDynamicConceptProviderConcept 的 [NotifyParentChange](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifyparentchange)

动态概念提供程序的 NotifyParent 方法是对对象的单个父模型执行静态操作时由核心数据模型进行的回调。 对于添加的任何给定父模型，将在第一次添加称为父模型时调用此方法，并在删除父模型时第二次调用。 

IDynamicConceptProviderConcept 的 [NotifyDestruct](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idynamicconceptproviderconcept-notifydestruct)

动态概念提供程序的 NotifyDestruct 方法是核心数据模型在销毁作为动态概念提供程序的对象的析构时进行的回调。 它向需要它的客户提供额外的清理机会。 

--

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

本主题是一系列文章的一部分，其中描述了可从 c + + 访问的接口，如何使用它们来生成基于 c + + 的调试器扩展，以及如何利用其他数据模型构造 (例如： JavaScript 或 NatVis) 从 c + + 数据模型扩展。

[调试器数据模型 C++ 概述](data-model-cpp-overview.md)

[调试器数据模型 C++ 接口](data-model-cpp-interfaces.md)

[调试器数据模型 C++ 对象](data-model-cpp-objects.md)

[调试器数据模型 C++ 的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 C++ 的概念](data-model-cpp-concepts.md)

[调试器数据模型 C++ 脚本](data-model-cpp-scripting.md)


 

