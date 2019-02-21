---
title: 扩展框架
description: 扩展框架
ms.assetid: 37a0fd70-0c88-414f-b4e3-afd641f1c667
keywords:
- Windows 设备测试框架 WDK，扩展 WDTF
- WDTF WDK，扩展 WDTF
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- Windows 设备测试框架 WDK 示例
- WDTF WDK 示例
- SimpleIO 向导 WDK WDTF
- 操作接口 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad1ceebb1450740034b8b80d21462843c1f606d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519443"
---
# <a name="extending-the-framework"></a>扩展框架


WDTF 构建为可扩展。 扩展性是三种不同方式，可能的如下图所示。

![说明 wdtf 方案模型关系图](images/wdtf-scenariomodel.gif)

以下列表介绍了三种扩展性方法，按顺序的难度：

-   **修改示例脚本**。 此方法与在上图中的绿色显示。 您可以选择一个提供 WDTF[示例脚本](sample-wdtf-scenarios.md)和修改为你的方案。 此外可以[创建 WDTF 方案](creating-wdtf-scenarios.md)从零开始。

-   **实现的现有** [**操作接口**](https://msdn.microsoft.com/library/windows/hardware/ff538355)**，如**SimpleIO。 此方法与在上图中的黄色显示。 您可以实现现有操作接口来扩展接口函数的目标类型。 如果为你的设备类型实现 SimpleIO，所有的现有基于 WDTF 的方案会自动开始执行你的设备的 I/O 验证。

    WDTF 提供 Microsoft Visual Studio 模板，以帮助实现 SimpleIO。 有关详细信息，请参阅[编写你的设备插件 WDTF SimpleIO](writing-a-wdtf-simpleio-plug-in-for-your-device.md)。

-   **创建 （，然后实现） 的新** [**操作接口**](https://msdn.microsoft.com/library/windows/hardware/ff538355)。 此方法会显示在上图中的红色。 如果 WDTF 提供的功能不足以构建你的基于组件的方案，可以使用 WDTF 若要创建新的组件。

    此方法是三种方法最困难的因为它需要[COM 接口的设计技巧](com-interface-design-skills.md)。 您必须能够设计和实现您的功能的简单抽象的使用 COM 自动化接口。

 

 




