---
title: 3D 制造的打印架构关键字
description: 3D 制造的打印架构关键字是打印架构规范的补充规范。
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2a8788ce090862dedb67bab42738a0e5f8befd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788023"
---
# <a name="print-schema-keywords-for-3d-manufacturing"></a>3D 制造的打印架构关键字

3D 制造的打印架构关键字是 [打印架构规范](https://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)的补充规范。 此规范需要了解在打印架构规范中定义的一组约定，尤其是该规范的第1部分和第3部分。 此规范包含的打印架构关键字是打印架构规范第2部分的3D 制造模拟。 它介绍了3D 制造设备的开发人员在打印架构的上下文中定义其设备功能时所使用的 XML 关键字。

此规范的主要目标是确保独立创建的软件和硬件系统的互操作性，为3D 制造设备生成或使用打印架构内容。 通常，这些软件和硬件系统通过 Windows 打印基础结构来发现彼此。

了解此规范需要可扩展标记语言 (XML) 和 XML 命名空间规范的工作知识。 完全了解还可能需要了解有关3D 制造部门中常见术语和过程的域知识，尽管每个努力都可以最大程度地减少此类依赖。

此规范中包含的信息可能会发生更改。 为了确保其在发布时的准确性，已经完成了每个工作。

## <a name="how-this-specification-is-organized"></a>如何组织此规范

| 部分                                                                     | 说明                                                                                                |
|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| [3D 制造关键字概述](3d-manufacturing-keywords-overview.md) | 提供3D 制造的打印架构关键字的基本概述、设计和使用情况信息。 |
| [设备控制关键字](device-control-keywords.md)                       | 这些关键字用于向3D 制造设备提供控制。                               |
| [材料关键字](material-keywords.md)                                   | 这些关键字介绍了用于创建3D 对象的设备中的原始材料。                          |
| [输出关键字](output-keywords.md)                                       | 这些关键字用于描述给定3D 制造作业的实际输出过程。          |
| [打印架构术语表](print-schema-glossary.md)                           | 提供此规范中使用的术语的定义。                                                 |
| [PrintCapabilities 文档示例](example-printcapabilities-document.md) | 提供一个示例 PrintCapabilities 文档。                                                            |
| [PrintTicket 文档示例](example-printticket-document.md)             | 提供一个示例 PrintTicket 文档。                                                                  |
| [打印架构参考](print-schema-references.md)                       | 提供对行业标准、规范和技术文章的参考。                         |

## <a name="document-conventions"></a>文档约定

除非另有说明，否则语法说明以 RFC 4234 中定义的 ABNF 格式表示。

术语表术语的格式设置为 *斜体* 。

语法说明和代码在类型中进行了格式设置 `monospace` 。

## <a name="language-notes"></a>语言备注

在此规范中，用于定义每个要求的重要性的单词以大写形式编写。 在 RFC 2119 中，将根据其定义使用这些词，并在下面重现它们各自的含义：

一定. 此词或形容词 "REQUIRED" 表示该项是规范的绝对要求。

决不. 此词或形容词 "建议" 是指在特定情况下可能存在用于忽略此项目的合理原因，但应理解完全含义，并在选择其他课程之前仔细权衡。

有助于. 此词或形容词 "OPTIONAL" 表示此项是真正可选的。 例如，一个实现可以选择包含项，因为特定的 marketplace 或方案需要它，或者是因为它可增强产品。 另一实现可能会忽略同一项。

## <a name="software-conformance"></a>软件一致性

本文档中的要求表示为格式要求，而不是实现要求。 有关 PrintTicket 和 PrintCapabilities 文档的其他要求，请参阅打印架构规范。

## <a name="implementation-license-agreement"></a>实现许可协议

有关详细信息，请参阅 SDK 许可协议的条款。
