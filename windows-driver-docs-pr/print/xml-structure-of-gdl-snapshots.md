---
title: GDL 快照的 XML 结构
description: GDL 快照的 XML 结构
keywords:
- GDL WDK，快照
- 快照 WDK GDL，结构
- 分析器 WDK GDL，快照
- GDL WDK，数据树
- 数据树 WDK GDL
- GDL WDK，项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a44a8acfecdb4b79f58dfb3b9aea623ff645e6c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785747"
---
# <a name="xml-structure-of-gdl-snapshots"></a>GDL 快照的 XML 结构


XML 快照是 GDL 数据树的子集，其中包含满足客户端提供的配置的那些交换机和案例分支。 数据树是由所有 GDL 数据条目构成的树，其中某些数据条目可能包含配置依赖项。 有关配置依赖项的详细信息，请参阅 [创建 GDL Configuration-Dependent 数据](creating-gdl-configuration-dependent-data.md)。

除了发出 XML 快照外，GDL 分析器还可以生成一个单独的 XSD 架构，用于描述快照的整体结构。 此架构还包含 GDL 模板定义的枚举数据类型的定义。 如果需要，客户端可以使用这些定义对快照中的所有基元数据类型执行架构验证。 如果未执行架构验证，则在加载 DOM 树时将不检查枚举的有效性;不需要执行此检查，因为 GDL 分析器执行其自身的枚举有效性检查。

为有效的 XML 文档，快照包含一个根元素： &lt; SnapshotRoot &gt; 。 此元素表示 GDL 树的根上下文。 &lt;SnapshotRoot &gt; 元素可以包含子 &lt; 构造 &gt; 或 &lt; GDL \_ 特性 &gt; 元素。 &lt;构造 &gt; 元素用于表示 GDL 构造， &lt; GDL \_ ATTRIBUTE &gt; 元素用于表示 GDL 特性。

每个 &lt; 构造 &gt; 元素都可以包含其他 &lt; 构造 &gt; 和 &lt; GDL \_ 特性 &gt; 元素。 &lt;GDL \_ 特性 &gt; 元素仅保存与该特性相关联的值，并且不包含任何 &lt; 构造 &gt; 或 &lt; GDL \_ 特性 &gt; 元素。 &lt;如果将 \_ &gt; 值定义为 GDL 复合数据类型，则 GDL 属性值可以直接显示为 &lt; 非复合数据类型的 GDL attribute 元素的字符数据内容， \_ &gt; 或者可由一个或多个子元素表示。

如果 GDL 分析器无法将属性与用于定义属性值的数据类型的模板关联，或者如果找到的值不符合声明的数据类型，则 &lt; \_ XML 快照中的相应 GDL attribute &gt; 元素将包含一个 &lt; CDATA &gt; 节，其中包含 GDL 文件中指定的原始值。

对于快照，GDL 支持以下类型的架构元素。

-   [Root](gdl-schema-root-element.md)

-   [构造](gdl-schema-construct-element.md)

-   [Attribute](gdl-schema-attribute-element.md)

以下主题介绍 XML 快照架构中使用的其他数据类型：

[枚举和 XSD 定义的数据类型](enumerations-and-xsd-defined-data-types.md)

[数据类型包装器](data-type-wrappers.md)

有关 XML 快照架构中的命名空间的详细信息，请参阅 [Xml 快照命名空间](xml-snapshot-namespaces.md)。

有关 XML 快照中字符数据的信息，请参阅以下主题：

[XML 架构换行符转换](xml-schema-linebreak-translations.md)

[XML 快照中的 Unicode 表示形式](unicode-representations-in-xml-snapshots.md)

[针对快照中允许的字符施加的 XML 限制](xml-restrictions-on-allowed-characters-in-snapshots.md)

 

 




