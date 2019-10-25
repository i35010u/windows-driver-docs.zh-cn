---
title: 扩展框架
description: 扩展框架
ms.assetid: 37a0fd70-0c88-414f-b4e3-afd641f1c667
keywords:
- Windows 设备测试框架 WDK，扩展 WDTF
- WDTF WDK，扩展 WDTF
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- Windows 设备测试框架 WDK，示例
- WDTF WDK，示例
- SimpleIO 向导 WDK WDTF
- 操作接口 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b7bca0282f495659ac169a470225d88d1463e69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823497"
---
# <a name="extending-the-framework"></a>扩展框架


WDTF 是为可扩展而构建的。 如下图所示，可以通过三种不同的方式实现扩展性。

![阐释 wdtf 方案模型的关系图](images/wdtf-scenariomodel.gif)

以下列表按难点说明了这三种扩展性方法：

-   **修改示例脚本**。 此方法在上图中显示为绿色。 你可以获取 WDTF 提供的[示例脚本](sample-wdtf-scenarios.md)之一，并修改它以适合你的方案。 你还可以从头开始[创建 WDTF 方案](creating-wdtf-scenarios.md)。

-   **实现现有的**[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) **，如**SimpleIO。 此方法在上图中显示为黄色。 您可以实现现有的操作接口，以扩展该接口所运行的目标的类型。 如果为设备类型实现 SimpleIO，则所有基于 WDTF 的现有方案将自动开始对设备执行 i/o 验证。

    WDTF 提供了一个 Microsoft Visual Studio 模板来帮助实现 SimpleIO。 有关详细信息，请参阅[编写设备的 WDTF SimpleIO 插件](writing-a-wdtf-simpleio-plug-in-for-your-device.md)。

-   **创建（然后实现）新的**[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 此方法在上图中以红色显示。 如果 WDTF 提供的功能不足以构造基于组件的方案，则可以使用 WDTF 来创建新组件。

    此方法最难实现这三种方法，因为它需要[COM 接口设计技巧](com-interface-design-skills.md)。 你必须能够使用 COM 自动化接口设计和实现功能的简单抽象。

 

 




