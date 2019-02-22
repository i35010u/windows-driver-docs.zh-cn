---
title: 打印三维生产的架构关键字
description: 3D 制造的打印架构关键字是打印架构规范的补充规范。
ms.assetid: DC54C326-31AE-43C9-AF0D-A3A64DAEF1F2
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: b535c6ae5354e698d04fd245f748e2afbb3c8252
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543537"
---
# <a name="print-schema-keywords-for-3d-manufacturing"></a>打印三维生产的架构关键字


3D 制造的打印架构关键字是一种补充到规范[打印架构规范](http://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)。 此规范需要了解的一组特定第 1 部分和该规范的第 3 部分中的打印架构规范中定义的约定。 此规范包含制造的打印架构规范的第 2 部分模拟 3D 打印架构关键字。 它描述了 XML 关键字的 3D 制造设备的开发人员用于打印架构的上下文中定义其设备的功能。

此规范的主要目标是确保互操作性的独立创建生成或使用打印架构的软件和硬件系统 3D 制造设备的内容。 通常情况下，这些软件和硬件系统发现彼此通过 Windows 打印基础结构。

要了解本规范需要的可扩展标记语言 (XML) 和 XML Namespace 规范的应用知识。 虽然每项工作变得尽量减少这种依赖性，全面了解可能还需要域知识的常用术语和 3D 生产部门内的过程。

此规范中包含的信息会发生变化。 每项工作进行发布时确保其准确性。

## <a name="how-this-specification-is-organized"></a>此规范的组织方式


| 部分                                                                      | 描述                                                                                                |
|------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| [3D 生产关键字概述](3d-manufacturing-keywords-overview.md) | 提供三维制造的打印架构关键字的基本概述、 设计和使用情况信息。 |
| [设备控制关键字](device-control-keywords.md)                       | 这些关键字用于提供对 3D 制造设备的控制。                               |
| [材料关键字](material-keywords.md)                                   | 这些关键字描述原始材料中用于创建三维对象的设备。                          |
| [输出关键字](output-keywords.md)                                       | 这些关键字用于描述给定 3D 生产作业的实际输出进程。          |
| [打印架构术语表](print-schema-glossary.md)                           | 为此规范中使用的术语提供定义。                                                 |
| [PrintCapabilities 文档示例](example-printcapabilities-document.md) | 提供了一个示例 PrintCapabilities 文档。                                                            |
| [PrintTicket 文档示例](example-printticket-document.md)             | 提供了一个示例 PrintTicket 文档。                                                                  |
| [打印架构引用](print-schema-references.md)                       | 提供了对行业标准、 规范和技术文章的引用。                         |


## <a name="document-conventions"></a>文档约定


除非另行说明，语法进行了说明中 RFC 4234 定义以 ABNF 格式表示。

术语表术语的格式为*斜体*类型。

语法说明和代码中设置的格式`monospace`类型。

## <a name="language-notes"></a>语言备注


在此规范中，用于定义每个需求的重要性的单词是用大写。 这些单词根据其定义根据 RFC 2119 中并且下面重新生成它们各自的含义是：

必须。 此词或形容词"需要，"意味着该项目已规范的是绝对要求。

应。 此词或形容词"建议、"意味着可能存在正当理由特别情况下，若要忽略此项，但应了解所有隐含意义并选择不同过程之前仔细权衡该情况。

5 月。 此词或形容词"OPTIONAL，"表示此项是真正可选的。 例如，一种实现可以选择包含的项，因为特定市场或方案需要它，或者因为它可增强产品。 另一个实现可能忽略同一项目。

## <a name="software-conformance"></a>软件符合性


本文档中的要求表示为格式要求，而非实现要求。 请参阅其他要求通常要求生成者和使用者的 PrintTicket 和 PrintCapabilities 文档打印架构规范。

## <a name="implementation-license-agreement"></a>实现许可协议


请参阅 SDK 许可协议的条款的详细信息。






