---
title: 测试 BDA 驱动程序使用 BDA 筛选器
description: 测试 BDA 驱动程序使用 BDA 筛选器
ms.assetid: 136810b7-9378-482b-8e21-a7eae0142909
keywords:
- 广播驱动程序体系结构 WDK AVStream，测试驱动程序
- BDA WDK AVStream，测试驱动程序
- 测试驱动程序 WDK，BDA
- DirectShow 筛选器 WDK AVStream
- 关系图编辑器 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2a9dec9af2e17292f22cb8ab242bc95c6c3c579
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555732"
---
# <a name="testing-bda-drivers-using-bda-filters"></a>测试 BDA 驱动程序使用 BDA 筛选器





可以使用 DirectShow 筛选器关系图编辑器 (*Graphedt.exe*)，以便可以测试你的组件在筛选器关系图中插入 BDA 组件的 DirectShow 筛选器实例。 您可以从 Microsoft Windows Driver Kit (WDK) 获取图形编辑器。

可以使用关系图编辑器执行基本测试的 BDA 组件，例如，连接到关系图中的筛选器类型的其他 pin 组件的筛选器实例公开的 pin。

若要使用关系图编辑器进行全面测试 BDA 组件的功能，必须生成开头 BDA 网络提供程序筛选器，包含 BDA 组件中，筛选器实例和呈现时，在至少一个信号分离器筛选器 （通过的筛选器关系图数据包标识符 (PID) 筛选器） 到传输的信息筛选器 (TIF)。 使用图形编辑器的最大问题是没有专用的应用程序来提交通过发出的请求**ITuner**网络提供程序筛选器实现的接口。 但是，网络提供程序筛选器具有关联的属性页提供某些限制的能够练习**ITuner**接口。

 

 




