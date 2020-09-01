---
title: GDL 体系结构
description: GDL 体系结构
ms.assetid: 3e796218-ab2a-40a7-a0e3-caeec5c6656e
keywords:
- GDL WDK，体系结构
- 创建快照 WDK GDL
- 快照 WDK GDL，创建快照
- 分析器 WDK GDL，通过 IPrintCoreHelperUni 访问分析器
- GDL WDK，架构
- GDL WDK，快照
- 体系结构 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54269290e93530851ec7b6bc5db1c65b6f66c299
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217157"
---
# <a name="gdl-architecture"></a>GDL 体系结构


本主题介绍 (GDL) 的泛型描述符语言的体系结构。

对于每个 GDL 数据集，应该定义一个 [GDL 架构](gdl-schemas.md) 来描述数据的格式。 包含数据集的每个文件都引用 GDL 架构。 此架构允许 GDL 分析器验证数据集是否符合该架构，并在构造快照时执行任何指定的转换。 对于在 GPD 中定义的所有数据，Microsoft 提供了标准架构。 此外，通过分析程序，您可以将一些数据定义为可配置。 其他数据可以通过某种方式进行描述，使其依赖于所使用的配置。

该规范可以转换为 GDL 架构。 包含数据集的每个文件都引用 GDL 架构。 此架构使 GDL 分析器能够验证数据集是否符合架构，并在构造快照时执行任何指定的转换。

在定义了数据集和架构之后，客户端可以通过指定不同的配置，从单个数据集创建多个视图或 [快照](gdl-snapshots.md)。 对于 Unidrv 配置和呈现插件，客户端可以通过 [IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni) 接口中的方法来访问快照。 GDL 分析器将加载在数据集中指定的架构，并验证该数据集是否符合其架构。 如果数据集不符合，则分析器将指示分析文件失败。

在定义了数据集和架构之后，客户端可以通过指定配置来创建数据集的快照：

1.  此插件通过[**IPrintOemUI：:P ublishdriverinterface**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)方法获取指向**IPrintCoreHelperUni**接口的指针。

2.  此插件通过调用 [**IPrintCoreHelperUni：： CreateGDLSnapshot**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperuni-creategdlsnapshot) 或 [**IPrintCoreHelperUni：： CreateDefaultGDLSnapshot**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperuni-createdefaultgdlsnapshot)请求访问快照。 如果该插件调用了 **CreateGDLSnapshot**，则调用方提供 DEVMODE 结构，该结构包含分析器用于确定快照视图的配置。

3.  GDL 分析器加载在数据集中指定的架构，并验证该数据集是否符合其架构。 如果数据集不符合，则将发出错误消息。

4.  GDL 分析器从 GDL 源文件创建内部数据结构，并根据提供的配置和架构中的处理指令确定相应的视图。

5.  分析器 (处理的数据条目的 *快照*) 创建 XML 表示形式。 此 XML 快照作为流返回到插件。

如果省略了架构，则分析器将只执行架构验证，快照值将在快照中表示为最初在 GDL 源文件中定义的字节字符串。

**注意**   **PublishDriverInterface**方法也是**IPrintOemUni**接口和其他接口的一部分。 因此插件不一定从 IPrintOemUI 获取 helper 接口 [**：:P ublishdriverinterface**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)。 它可以从 **IPrintOemUni：:P ublishdriverinterface** 或其他位置获取 helper 接口，具体取决于插件实现的接口类型。

 

 

