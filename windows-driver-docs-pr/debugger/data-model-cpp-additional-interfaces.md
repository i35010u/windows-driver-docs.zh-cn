---
title: 调试器数据模型 C++ 的其他接口
description: 本主题介绍与调试器 c + + 数据模型（如元数据、概念和对象枚举）关联的其他接口。
ms.date: 09/12/2018
ms.openlocfilehash: beafff8f951b7ed912b18b673fd289de0b815845
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206821"
---
# <a name="debugger-data-model-c-additional-interfaces"></a>调试器数据模型 C++ 的其他接口

本主题介绍与调试器 c + + 数据模型关联的一些附加接口，如元数据、概念和对象枚举。

## <a name="span-idmetadatainterfacesspan-debugger-data-model-metadata-interfaces"></a><span id="metadatainterfaces"></span> 调试器数据模型元数据接口

数据模型中的核心观念之一是，对象 (尤其是合成一个) 是键/值/元组的字典。 每个密钥都可以有与之关联的元数据的整个存储区，该存储区描述密钥及其潜在值周围的各种情况。 请注意，元数据不会以任何方式更改密钥的值。 它只是与键及其值相关联的辅助信息，这可能会影响该项的表示形式或其他关联特性及其值。 

在某些情况下，元数据存储区并不是与数据模型中的对象实质上的键/值元元组不同。 不过，它在此视图中进行了简化。 元数据存储区由 IKeyStore 接口表示。 同时还包含键/值/元数据元组的集合，但可以对元数据密钥存储和模型对象执行的操作有限制： 

- 一个密钥存储只能有一个父存储，而不能具有父模型的任意链。
- 密钥存储没有任何概念。 它只能包含键/值/元组的字典。 这意味着密钥存储中的密钥是静态的。 动态语言系统不能按需创建它们。
- 根据约定，元数据定义的密钥存储中的值仅限于基本值 (内部函数和属性访问器) 

尽管密钥存储可以有任意数量的 (和任意命名密钥) ，但仍存在一些已定义语义值的名称。 目前，这些名称为： 

键名 | 值类型 | 说明
|--------------|------------------|--------------|
PreferredRadix | 整数：2、8、10或16 | 指示应在其中显示序数值的基数
PreferredFormat | Integer： PreferredFormat 枚举定义的 | 指示用于显示值的首选格式设置类型
PreferredLength | Integer | 对于数组和其他容器，指示默认情况下应显示的元素数
FindDerivation | 布尔 | 指示在使用 (例如：显示) 之前，调试宿主是否应对值执行派生类型分析
帮助 | String | 用于密钥的工具提示文本，用户界面可以提供相应的有用方式。
ActionName | String | 指示给定方法 (一个不采用任何参数，并且不返回任何值) 为操作。 在元数据中指定操作的名称。 用户界面可以利用此名称来显示上下文菜单或其他相应接口中的选项
ActionIsDefault | 布尔 | 仅在指定 ActionName 键时有效，指示这是对象的默认操作。
ActionDescription | String | 仅当指定了 ActionName 键时，这将提供操作的工具提示样式说明。 用户界面可以以适当的方式提供此类文本。

请注意，元数据存储区中的密钥可以有自己的元数据 (ad infiniteum) ，目前不会使用此类。 大多数调用方将为 IKeyStore 接口上的方法中的任何元数据参数指定 null。 

**核心元数据接口： IKeyStore**

IKeyStore 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IKeyStore, IUnknown)
{
   STDMETHOD(GetKey)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(SetKey)(_In_ PCWSTR key, _In_opt_ IModelObject* object, _In_opt_ IKeyStore* metadata) PURE;
   STDMETHOD(GetKeyValue)(_In_ PCWSTR key, _COM_Errorptr_opt_ IModelObject** object, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(SetKeyValue)(_In_ PCWSTR key, _In_ IModelObject* object) PURE;
   STDMETHOD(ClearKeys)() PURE;
}
```

[GetKey](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-getkey)

GetKey 方法类似于 IModelObject 上的 GetKey 方法。 它将返回指定键的值（如果它存在于密钥存储区或密钥存储的父存储区中）。 请注意，如果键的值为属性访问器，则不会在属性访问器上调用 GetValue 方法。 将返回装箱到 IModelObject 中的实际 IModelPropertyAccessor。 通常，出于此原因，客户端将调用 GetKeyValue。 

[SetKey](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-setkey)

SetKey 方法类似于 IModelObject 上的 SetKey 方法。 这是唯一一种可在密钥存储中创建密钥并将其与之相关联的方法。 

[GetKeyValue](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-getkeyvalue)

GetKeyValue 方法是客户端将进行的第一种方法，以便在元数据存储中查找特定键的值。 如果存储区中存在由密钥参数指定的密钥 (或其父存储) ，则将返回该密钥的值以及与之关联的所有元数据。 如果该注册表项的值是 (装箱到 IModelObject) 中的属性访问器，则 GetKeyValue 将自动调用属性访问器的 GetValue 方法，并返回该属性的基础值。 

[SetKeyValue](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-setkeyvalue)

SetKeyValue 方法类似于 IModelObject 上的 SetKeyValue 方法。 此方法无法在元数据存储区中创建新密钥。 如果有密钥参数所指示的现有密钥，则会按指示设置其值。 如果该键是属性访问器，则将对属性访问器调用 SetValue 方法，以便设置基础值。 请注意，元数据在创建后通常是静态的。 在元数据密钥存储上使用此方法应很少发生。 

[ClearKeys](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeystore-clearkeys)

ClearKeys 方法类似于 IModelObject 上的 ClearKeys 方法。 它将从给定的元数据存储区中移除每个键。 此方法对任何父存储区不起作用。 


## <a name="span-idobjectspan-object-enumeration-in-the-data-model"></a><span id="object"></span> 数据模型中的对象枚举

**枚举数据模型中的对象**

数据模型中有两个核心密钥枚举接口： IKeyEnumerator 和 IRawEnumerator。 虽然这两个核心接口都是两个核心接口，但它们可用于使用以下三种样式之一枚举对象： 

*键* -可以通过调用 EnumerateKeys 来获取 IKeyEnumerator 接口，以便枚举对象的键及其值/元数据，而无需解析任何基础属性访问器。 这种类型的枚举可以返回装箱到 IModelObjects 中的原始 IModelPropertyAccessor 值。

*值* -可通过调用 EnumerateKeyValues 或 EnumerateRawValues 来获取 IKeyEnumerator 和 IRawEnumerator 接口，以便枚举对象上的键/原始值及其值/元数据。 枚举中提供的任何属性访问器都将在此类枚举过程中通过调用基础 GetValue 方法自动解析。

*引用* -可以通过调用 EnumerateKeyReferences 或 EnumerateRawReferences 来获取 IKeyEnumerator 和 IRawEnumerator 接口，以便枚举对对象上的键/原始值的引用。 可以保存此类引用，并在以后使用此类引用获取或设置基础键或原始值。

**KeyEnumerator：综合密钥的枚举**

IKeyEnumerator 接口是单个接口，用于枚举实例对象内的键、值或引用)  (，以及父模型链中所有关联的父模型。 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IKeyEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR* key, _COM_Errorptr_opt_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

[重置](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeyenumerator-reset)

Reset 方法会将枚举数重置为首次获取时所处的位置 (例如：) 枚举中的第一个元素之前。 对 GetNext 的后续调用将返回第一个枚举密钥。 

[GetNext](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ikeyenumerator-getnext)

GetNext 方法都向前移动枚举器并在枚举中返回该位置处的键。


**IRawEnumerator：本机或基础语言 () 构造的枚举**

IRawEnumerator 接口是一个单一接口，用于枚举对象内的值或引用)  (，该对象表示调试目标的地址空间内的本机构造。 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IRawEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_opt_ BSTR* name, _Out_opt_ SymbolKind *kind, _COM_Errorptr_opt_ IModelObject** value) PURE;
}
```

[重置](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-irawenumerator-reset)

Reset 方法会将枚举数重置为首次获取时所处的位置 (例如：) 枚举中的第一个元素之前。 对 GetNext 的后续调用将返回第一个枚举的本机/语言构造。 

[GetNext](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-irawenumerator-getnext)

GetNext 方法都向前移动枚举器，并在枚举中的该位置返回本机/语言构造。 

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

本主题是一系列文章的一部分，其中描述了可从 c + + 访问的接口，如何使用它们来生成基于 c + + 的调试器扩展，以及如何利用其他数据模型构造 (例如： JavaScript 或 NatVis) 从 c + + 数据模型扩展。

[调试器数据模型 C++ 概述](data-model-cpp-overview.md)

[调试器数据模型 C++ 接口](data-model-cpp-interfaces.md)

[调试器数据模型 C++ 对象](data-model-cpp-objects.md)

[调试器数据模型 C++ 的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 C++ 的概念](data-model-cpp-concepts.md)

[调试器数据模型 C++ 脚本](data-model-cpp-scripting.md)