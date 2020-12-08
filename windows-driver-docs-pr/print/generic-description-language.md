---
title: 通用描述语言
description: 通用描述语言
keywords:
- 打印机配置 WDK，GDL 文件
- 文本文件 WDK GDL 文件
- 一般描述语言 WDK
- GDL WDK
- GDL WDK，关于
- 一般打印机说明 WDK Unidrv
- GPD WDK
- 打印机驱动程序 WDK，一般描述语言
- 打印机驱动程序 WDK，将数据转换为 XML
- 将数据转换为 XML WDK GDL
- 将数据转换为 XML WDK GDL
- GDL WDK，分析器
- GDL WDK，快照
- 快照 WDK GDL
- GDL WDK，指令
- 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1278be917efbab9a5bf25ef973cde976bf8f465
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835869"
---
# <a name="generic-description-language"></a>通用描述语言


一般描述语言 (GDL) 定义用于表达分层结构化数据的语法。 GDL 还使制造商和使用者可以协作定义一个可用于标准化数据表达方式的架构。 此架构可用于验证数据的结构和格式，并将数据转换为其他格式 (例如 XML) 。

Microsoft 提供 [GDL 分析器](gdl-parser.md) 和关联的 *分析器筛选器，这些筛选器* 访问和处理源数据文件中的数据，并将其转换为 [GDL 语法](gdl-syntax.md) 定义的层次结构数据。 GDL 支持复杂的数据集、面向对象的架构，这些架构定义了此数据的结构和处理，并提供了由供应商轻松扩展的机制。

GDL 设计为通用打印机说明的超集 ([GPD](introduction-to-gpd-files.md)) 语言，用于描述 Unidrv 微型驱动程序的打印机功能。

GDL 具有以下主要功能：

-   GDL 与 GPD 旧格式向后兼容。

-   GDL 可任意扩展。 也就是说，任何人都可以添加自定义属性和构造。

-   GDL 使用模板提供数据结构。

-   GDL 使用预处理器指令和参数驱动的配置来提供灵活的链接和条件。

-   GDL 分析数据输入并将 XML 流返回给客户端。

当[GDL 分析器](gdl-parser.md)分析[GDL 源文件](gdl-source-files.md)中的数据时，分析器将维护一个分层数据结构。 客户端通过 [快照](gdl-snapshots.md)间接访问已分析的数据结构。 *快照* 是处于特定状态的数据的表示形式。 此状态是通过 [配置](gdl-configurations.md)指定的。 在 GDL 分析器的当前实现中，快照以 XML 形式表示，并且可以使用 XML 工具访问快照中的数据。

除了数据条目外，GDL 分析器还 [识别)  (](gdl-directives.md) 的关键字。 指令包括 [预处理器](gdl-source-file-preprocessor-directives.md)、 [宏](gdl-directives-for-macros.md)、 [命名空间](gdl-directives-for-namespaces.md)、 [模板](gdl-directives-for-templates.md)和 [配置](gdl-directives-for-configurations.md)等类别。

以下各节提供了有关 GDL 的详细信息：

[GDL 体系结构](gdl-architecture.md)

[GDL 编程指南](gdl-programming-guide.md)

[GDL 参考](gdl-reference.md)

[GDL 示例](gdl-examples.md)

 

 




