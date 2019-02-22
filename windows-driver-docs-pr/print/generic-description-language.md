---
title: 通用描述语言
description: 通用描述语言
ms.assetid: 818037fd-90bb-46dd-a2e3-239d57ed5fcf
keywords:
- 打印机配置 WDK、 GDL 文件
- 文本文件 WDK GDL 文件
- 通用描述语言 WDK
- GDL WDK
- GDL WDK，关于
- 通用打印机说明 WDK Unidrv
- GPD WDK
- 打印机驱动程序 WDK，泛型描述语言
- 打印机驱动程序 WDK、 数据转换为 XML
- 将数据转换成 XML WDK GDL
- 将数据转换为 XML WDK GDL
- GDL WDK 分析器
- GDL WDK 快照
- 快照 WDK GDL
- GDL WDK 指令
- WDK GDL 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c94725649daf146315fbd95109b4e0b4ee4866c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519940"
---
# <a name="generic-description-language"></a>通用描述语言


通用描述语言 (GDL) 定义用来表示层次结构上结构化的数据的语法。 GDL 还使制造商和使用者能够以协作方式定义可用于表示数据的方式实现标准化的架构。 若要验证的结构和数据的格式和指导数据转换为其他格式 （如 XML)，可以使用此架构。

Microsoft 提供了[GDL 分析器](gdl-parser.md)关联*分析器筛选器*，其中来自源数据的访问和处理数据文件，并将其转换为层次结构数据的[GDL 语法](gdl-syntax.md)定义。 GDL 支持复杂数据集，定义的结构和处理此数据，以及用于轻松扩展由供应商的机制的面向对象的架构。

GDL 设计为通用打印机说明的超集 ([GPD](introduction-to-gpd-files.md)) 语言，用于描述 Unidrv 微型驱动程序的打印机功能。

GDL 具有以下主要功能：

-   GDL 能够向后兼容 GPD 旧格式。

-   GDL 是任意可扩展的。 也就是说，任何人都可以添加自定义属性和构造。

-   GDL 使用模板来提供数据结构。

-   GDL 使用预处理器指令和参数驱动的配置提供灵活的链接和条件。

-   GDL 分析数据输入，并返回到客户端的 XML 流。

时中的数据[GDL 源文件](gdl-source-files.md)由分析得到[GDL 分析器](gdl-parser.md)，分析器会维护分层数据结构。 客户端访问的已分析的数据结构通过间接[快照](gdl-snapshots.md)。 *快照*是某一特定状态中的数据的表示形式。 通过指定此状态[配置](gdl-configurations.md)。 在当前实现中的 GDL 分析器，快照表示为 XML，并可以通过使用 XML 工具访问快照中的数据。

除了数据条目 GDL 分析器可识别关键字 (这称为[指令](gdl-directives.md))。 指令包括类别如下所述[预处理器](gdl-source-file-preprocessor-directives.md)，[宏](gdl-directives-for-macros.md)，[命名空间](gdl-directives-for-namespaces.md)，[模板](gdl-directives-for-templates.md)，和[配置](gdl-directives-for-configurations.md)。

以下部分提供有关 GDL 的详细信息：

[GDL 体系结构](gdl-architecture.md)

[GDL 编程指南](gdl-programming-guide.md)

[GDL 引用](gdl-reference.md)

[GDL 示例](gdl-examples.md)

 

 




