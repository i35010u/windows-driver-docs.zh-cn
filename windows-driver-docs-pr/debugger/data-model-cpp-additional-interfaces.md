---
title: 调试器数据模型 c + + 其他接口
description: 本主题介绍与调试器的 c + + 数据模型，如元数据、 概念和对象的枚举相关联的其他接口。
ms.date: 10/05/2018
ms.openlocfilehash: 3c0a9f9f11accd8d78a90b110cfae38d77257412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546452"
---
# <a name="debugger-data-model-c-additional-interfaces"></a>调试器数据模型 c + + 其他接口

本主题介绍一些与调试器的 c + + 数据模型，如元数据、 概念和对象的枚举相关联的其他接口。

本主题是一系列用于描述可从 c + +、 如何使用它们来构建基于 c + + 调试器扩展，以及如何使访问接口的一部分使用的数据模型的其他构造 (例如：JavaScript 或 NatVis） 从 c + + 数据模型扩展插件。

---

[调试程序数据模型 c + + 概述](data-model-cpp-overview.md)

[调试器数据模型 c + + 接口](data-model-cpp-interfaces.md)

[调试器数据模型 c + + 对象](data-model-cpp-objects.md)

[调试器数据模型 c + + 其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 c + + 概念](data-model-cpp-concepts.md)

[C + + 编写脚本的调试程序数据模型](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>主题部分

本主题包含以下部分：

[调试器数据模型元数据接口](#metadatainterfaces)

[数据模型中的对象枚举](#object)

---

## <a name="span-idmetadatainterfacesspan-debugger-data-model-metadata-interfaces"></a><span id="metadatainterfaces"></span> 调试器数据模型元数据接口

核心概念数据模型中的一个是对象 （尤其是合成一个） 是元数据键/值元组的字典。 每个密钥可以有与之关联的介绍有很多事情周围的键和其可能值的元数据的整个存储库。 请注意，元数据不会以任何方式更改密钥的值。 它是仅辅助信息关联的键和其值，该值可能会影响此演示文稿或其他关联的特性的键和其值。 

在某种意义上，元数据存储区不是数据模型中的对象的本质的元数据键/值元组的差异。 它，但是，从简化此视图。 元数据存储区由 IKeyStore 接口表示。 同时还元数据键/值元组的集合，有什么可以完成与模型对象的元数据密钥存储限制： 

- 密钥存储只能有单个父存储区--它不能有一种任意的父模型链。
- 密钥存储中有没有概念。 它只能有元数据键/值元组的字典。 这意味着，密钥存储中存在的键是静态的。 它们可以创建按需动态语言系统。
- 仅显示约定中定义的元数据密钥存储的值被限制为基本值 （内部函数和属性访问器）

虽然密钥存储的密钥可以具有任意数量 （和任意命名），但在某些定义了语义值的名称。 目前，这些名称是： 

项名称 | 值类型 | 描述
|--------------|------------------|--------------|
PreferredRadix | 整数：2、 8、 10 或 16 | 指示一个序号值，应显示在哪个基数
PreferredFormat | 整数： 定义由 PreferredFormat 枚举 | 指示值的显示的首选格式设置类型
PreferredLength | 整型 | 有关数组和其他容器，指示应默认情况下显示的元素数量
FindDerivation | 布尔 | 指示是否调试主机应执行派生的类型分析的值在使用之前 (例如： 显示)
Help | 字符串 | 通过适当地有用的方法中的用户界面的键可以显示的工具提示样式的帮助文本。
ActionName | 字符串 | 指示给定的方法 （其中一个不采用任何参数，并不返回任何值） 操作。 在元数据中指定的操作的名称。 用户界面可使用此名称以显示上下文菜单或其他适当的接口中的选项
ActionIsDefault | 布尔 | 仅指定键，则的 ActionName 指示这是该对象的默认操作才有效。
ActionDescription | 字符串 | 唯一有效如果指定 ActionName 密钥，这样，该操作的工具提示样式说明。 可通过用户界面以相应地有帮助的方式展示此类文本。

请注意，虽然元数据存储区中的键可以有自己的元数据 (ad infiniteum)，目前尚无需使用此类。 大多数调用方将指定 IKeyStore 接口上的方法中的任何元数据参数为 null。 

**核心元数据接口：IKeyStore**

IKeyStore 接口定义，如下所示： 

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

[GetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-getkey)

GetKey 方法相当于 IModelObject GetKey 方法。 如果它存在于密钥存储或密钥存储父存储区中，它将返回指定键的值。 请注意，是否键的值属性访问器，GetValue 方法不会调用在属性访问器上。 将返回实际 IModelPropertyAccessor 到 IModelObject 装箱。 它是典型客户端将出于此原因调用 GetKeyValue。 

[SetKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-setkey)

Setkey 权限方法相当于 IModelObject 的 setkey 权限方法。 它是能够创建密钥并将元数据与它关联的密钥存储内的唯一方法。 

[GetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-getkeyvalue)

GetKeyValue 方法是为了在元数据存储区中查找特定项的值，客户端将转到第一种方法。 如果指定的密钥参数的键存在，则将在应用商店 （或它的父存储区） 中，返回该注册表项和与之关联的任何元数据的值。 如果键的值属性访问器 (装箱到 IModelObject IModelPropertyAccessor)，自动将 GetKeyValue 和返回的属性的基础值由调用属性访问器的 GetValue 方法。 

[SetKeyValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-setkeyvalue)

SetKeyValue 方法相当于 IModelObject SetKeyValue 方法。 此方法不能创建新的密钥元数据存储区中。 如果没有现有的密钥由键参数，则其值将设置所示。 如果对密钥进行属性访问器，SetValue 方法将调用在属性访问器上要设置的基础值。 请注意，元数据通常都是静态一次创建。 使用元数据密钥存储在此方法应很少。 

[ClearKeys](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeystore-clearkeys)

ClearKeys 方法相当于 IModelObject ClearKeys 方法。 它将从给定的元数据存储中删除每个键。 此方法不起任何父存储区上。 


## <a name="span-idobjectspan-object-enumeration-in-the-data-model"></a><span id="object"></span> 数据模型中的对象枚举

**枚举数据模型中的对象**

数据模型中有两个核心键的枚举接口：IKeyEnumerator 和 IRawEnumerator。 虽然这些都是两个核心接口，它们可用于枚举中一个三种样式的对象： 

*密钥*-IKeyEnumerator 接口才能获取通过调用 EnumerateKeys 以便枚举的键的对象并将其值/元数据，而不解决任何基础属性访问器。 这种样式的枚举可以返回到 IModelObjects 装箱的原始 IModelPropertyAccessor 值。

*值*-可以通过调用以便枚举对象并将其值/元数据中的原始键/值 EnumerateKeyValues 或 EnumerateRawValues 获取 IKeyEnumerator 和 IRawEnumerator 接口。 在此类枚举过程中，枚举中存在任何属性访问器通过调用基础的 GetValue 方法自动解决。

*引用*-IKeyEnumerator 和 IRawEnumerator 接口才能获取通过调用 EnumerateKeyReferences 或 EnumerateRawReferences 以便枚举对某个对象的原始键/值对的引用。 可以保存此类引用，并在以后使用要获取或设置基础密钥或原始值。

**KeyEnumerator:综合键的枚举**

IKeyEnumerator 接口的实例对象和其父模型链中的所有相关联的父模型中是 （通过键、 值或引用） 的所有键的枚举的单个接口。 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IKeyEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR* key, _COM_Errorptr_opt_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeyenumerator-reset)

重置方法将枚举数重置为它所处时首次获取的位置 (例如： 枚举中的第一个元素之前)。 GetNext 的后续调用将返回第一个枚举的键。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ikeyenumerator-getnext)

GetNext 方法都将枚举数向前移动，并返回该枚举中的位置处的键。


**IRawEnumerator:枚举 （C/c + +） 的本机或基础语言构造**

IRawEnumerator 接口是 （通过值或引用） 对象的表示的调试目标的地址空间中的本机结构中的所有本机/语言构造的枚举的单个接口。 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IRawEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_opt_ BSTR* name, _Out_opt_ SymbolKind *kind, _COM_Errorptr_opt_ IModelObject** value) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-irawenumerator-reset)

重置方法将枚举数重置为它所处时首次获取的位置 (例如： 枚举中的第一个元素之前)。 GetNext 的后续调用将返回第一个枚举的本机/语言构造。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-irawenumerator-getnext)

GetNext 方法都将枚举数向前移动，并返回该位置的枚举中的本机/语言构造。 


---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题

[调试程序数据模型 c + + 概述](data-model-cpp-overview.md)

[调试器数据模型 c + + 接口](data-model-cpp-interfaces.md)

[调试器数据模型 c + + 对象](data-model-cpp-objects.md)

[调试器数据模型 c + + 其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 c + + 概念](data-model-cpp-concepts.md)

[C + + 编写脚本的调试程序数据模型](data-model-cpp-scripting.md)

