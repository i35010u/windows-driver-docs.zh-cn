---
title: GDL 快照的 XML 结构
description: GDL 快照的 XML 结构
ms.assetid: 46051e45-da46-488c-9d70-2299954445be
keywords:
- GDL WDK 快照
- 快照 WDK GDL，结构
- 分析器 WDK GDL，快照
- GDL WDK，数据树
- 数据树 WDK GDL
- GDL WDK 条目
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28eda4cbe723ae5efeded569785b783fa3be5978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546061"
---
# <a name="xml-structure-of-gdl-snapshots"></a>GDL 快照的 XML 结构


XML 快照是包含满足客户端提供配置这些开关和用例分支 GDL 数据树的子集。 数据树是通过 GDL 数据条目，其中一些可能必须配置依赖关系的所有格式正确的树。 有关配置依赖关系的详细信息，请参阅[创建 GDL 配置依赖于数据](creating-gdl-configuration-dependent-data.md)。

除了 XML 快照，则生成 GDL 分析器还可以生成单独的 XSD 架构描述快照的整体结构。 此架构还包含 GDL 模板定义的枚举数据类型的定义。 这些定义使客户端所需的则快照中执行的所有基元数据类型的架构验证。 如果不执行架构验证，则加载 DOM 树; 时，枚举不会检查的有效性此检查不必要，因为 GDL 分析器执行其自身枚举有效性检查。

若要有效的 XML 文档，快照包含一个根元素：&lt;SnapshotRoot&gt;。 此元素表示 GDL 树的根上下文。 &lt;SnapshotRoot&gt;元素可以包含子&lt;构造&gt;或&lt;GDL\_特性&gt;元素。 &lt;构造&gt;元素用于表示一个 GDL 构造，并&lt;GDL\_特性&gt;元素用于表示 GDL 属性。

每个&lt;构造&gt;元素可以包含其他&lt;构造&gt;并&lt;GDL\_特性&gt;元素。 &lt;GDL\_特性&gt;元素包含与该属性相关联并不包含任何值&lt;构造&gt;或&lt;GDL\_属性&gt;元素。 &lt;GDL\_特性&gt;值可以显示为字符数据的内容直接&lt;GDL\_特性&gt;非复合数据类型的元素或其中一个可以表示或更多的子元素，如果值定义为 GDL 复合数据类型。

如果 GDL 分析器不能将属性与定义该属性的值的数据类型的模板或找到的值不符合相应的声明的数据类型&lt;GDL\_特性&gt;XML 快照中的元素将包含&lt;CDATA&gt;节，其中包含 GDL 文件中指定的原始值。

GDL 支持以下类型的架构元素生成的快照。

-   [Root](gdl-schema-root-element.md)

-   [构造](gdl-schema-construct-element.md)

-   [属性](gdl-schema-attribute-element.md)

下面的主题介绍在 XML 快照架构中使用的其他数据类型：

[枚举和 XSD 定义的数据类型](enumerations-and-xsd-defined-data-types.md)

[数据类型的包装](data-type-wrappers.md)

有关 XML 快照架构中的命名空间的详细信息，请参阅[XML 快照命名空间](xml-snapshot-namespaces.md)。

有关 XML 快照中的字符数据的信息，请参阅以下主题：

[XML 架构 Linebreak 翻译](xml-schema-linebreak-translations.md)

[XML 快照中的 Unicode 表示形式](unicode-representations-in-xml-snapshots.md)

[在快照中允许的字符的 XML 限制](xml-restrictions-on-allowed-characters-in-snapshots.md)

 

 




