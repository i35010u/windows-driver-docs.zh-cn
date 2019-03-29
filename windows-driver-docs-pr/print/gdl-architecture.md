---
title: GDL 体系结构
description: GDL 体系结构
ms.assetid: 3e796218-ab2a-40a7-a0e3-caeec5c6656e
keywords:
- GDL WDK，体系结构
- 创建快照 WDK GDL
- 快照 WDK GDL，创建快照
- 分析器 WDK GDL，通过 IPrintCoreHelperUni 访问分析器
- GDL WDK 架构
- GDL WDK 快照
- WDK GDL 体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e6ea7d05b5b01b4a6a3440041f5b76fd0a9aad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568575"
---
# <a name="gdl-architecture"></a>GDL 体系结构


本主题介绍的泛型描述符语言 (GDL) 的体系结构。

对于每个 GDL 数据集，则应定义[GDL 架构](gdl-schemas.md)来描述数据的格式。 包含的数据集的每个文件引用 GDL 架构。 此架构允许 GDL 分析器来验证数据集符合架构并构造快照时执行指定的任何转换。 对于 GPD 中定义的所有数据，Microsoft 提供了标准架构。 此外，分析器可以定义为可配置的一些数据。 其他数据可以采用的方式使它依赖于使用的配置中所述。

该规范可以转换为 GDL 架构。 包含的数据集的每个文件引用 GDL 架构。 此架构使 GDL 分析器来验证数据集符合架构并构造快照时执行指定的任何转换。

定义数据集和架构后，客户端可以创建多个视图，或[快照](gdl-snapshots.md)，从单个数据集通过指定不同的配置。 对于 Unidrv 配置和呈现插件，客户端可以通过在方法访问快照[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)接口... GDL 分析器将加载数据集中指定的架构，并验证数据集符合其架构。 如果数据集不符合，分析器将指示无法分析文件。

定义数据集和架构后，客户端可以通过指定一个配置创建数据集的快照：

1.  该插件获取指向的指针**IPrintCoreHelperUni**接口通过[ **IPrintOemUI::PublishDriverInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff554184)方法。

2.  插件的请求访问到通过调用快照[ **IPrintCoreHelperUni::CreateGDLSnapshot** ](https://msdn.microsoft.com/library/windows/hardware/ff552923)或[ **IPrintCoreHelperUni::CreateDefaultGDLSnapshot**](https://msdn.microsoft.com/library/windows/hardware/ff552917)。 如果插件调用**CreateGDLSnapshot**，调用方提供了一个 DEVMODE 结构，其中包括分析器使用来确定在快照视图的配置。

3.  GDL 分析器加载数据集中指定和验证数据集符合其架构的架构。 如果数据集不符合，将发出错误消息。

4.  GDL 分析器从 GDL 源文件创建的内部数据结构，并确定适当的视图基于架构中的提供和处理指令的配置。

5.  分析器创建的 XML 表示形式 (*快照*) 的已处理的数据条目。 到该插件以流的形式返回此 XML 快照...

如果省略架构，则分析器将只需执行架构验证和快照值将为快照中表示为最初 GDL 源文件中定义的字节的字符串。

**请注意**   **PublishDriverInterface**方法属于**IPrintOemUni**接口和其他接口。 因此插件不一定会从帮助程序接口[ **IPrintOemUI::PublishDriverInterface**](https://msdn.microsoft.com/library/windows/hardware/ff554184)。 它可以获取从帮助程序接口**IPrintOemUni::PublishDriverInterface**或其他位置具体取决于类型的接口，该插件的实现。

 

 

 




