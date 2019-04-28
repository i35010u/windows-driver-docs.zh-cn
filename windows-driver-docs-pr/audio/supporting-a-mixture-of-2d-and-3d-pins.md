---
title: 支持混合使用 2D 和 3D 引脚
description: 支持混合使用 2D 和 3D 引脚
ms.assetid: 26d98eca-b70a-4244-a7c3-d3a19930a96a
keywords:
- 硬件加速 WDK DirectSound、 2D 和 3D 固定混合
- 3D 混合 WDK 音频
- 2D 混合 WDK 音频
- pin WDK 音频 2D
- pin WDK 音频 3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048f7e3c4a3a3fa6a68f512d8e0f801d3f1745c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328577"
---
# <a name="supporting-a-mixture-of-2d-and-3d-pins"></a>支持混合使用 2D 和 3D 引脚


## <span id="supporting_a_mixture_of_2d_and_3d_pins"></span><span id="SUPPORTING_A_MIXTURE_OF_2D_AND_3D_PINS"></span>


如果您的 2D 和 3D 插针、 三维 pin 混合会加倍的 WDM 音频驱动程序支持使用作为 2D pin，但反之则不然。 当 DirectSound 需要 2D pin 时，它可以实现此目的，替换未使用的三维 pin，如果有来自驱动程序可用。 如果 DirectSound 需要三维 pin，但是，它继续搜索 pin 实例的驱动程序的列表，直到它找到 3D pin，忽略在搜索过程中遇到任何 2D pin。 DirectSound 检查在其中列出直到找到满足其要求的 pin 实例的顺序中的 pin 工厂的驱动程序的列表。

在报告的 2D pin 计数，您的驱动程序应指定 2D pin 实例数加上的 3D pin 实例数。 在报告的 3D pin 计数，您的驱动程序应忽略 2D pin 并指定仅 3D pin 实例数。

DirectSound 版本已经分发 Microsoft Windows 2000 和 Windows 98 中公开各种 2D 和 3D pin 的 pin 工厂处理存在已知的问题：DirectSound 错误地报告 3D pin count 是 2D pin 实例数加上的 3D pin 实例数。 此问题的解决方法解决方案是编写您的驱动程序，使其相互 2D 和 3D pin 隔离到两个单独的 pin 工厂。 一个工厂公开仅 2D 球瓶和其他工厂公开仅 3D 插针。

WDM 驱动程序后，DirectSound 正确地报告 2D pin 计数的 2D 和 3D 插针从两个工厂，计数之和它正确地报告 3D pin 计数为 3D 插针从一个 3D pin 工厂数。 公开时单独工厂 2D 和 3D pin，您的驱动程序应列出 3D pin 工厂之前的 2D pin 工厂。 这是必需的因为当 DirectSound 寻找 2D pin，它将使用它找到的第一次 2D 或 3D 插针和 DirectSound 检查驱动程序列出它们的顺序的 pin 工厂。 如果驱动程序首先列出 3D 工厂，它的风险具有 DirectSound 消耗的 3D pin 提供的不必要地使用它们来代替 2D pin。

总之，如果您的驱动程序将公开各种 2D 和 3D pin，它应遵循这些规则，以在早期版本的 DirectSound 上正确运行：

-   分别为 2D 和 3D 的 pin，提供两个单独的 pin 工厂。

-   列表 2D pin 之前的 3D pin 工厂的工厂。

这些替代方法是不必要的 DirectSound 较新版本。 上面所述的问题被解决 Windows Me 中和在 Windows XP 及更高版本。 它也被固定的 DirectSound 8，使用与早期 Windows 版本重新分发。 通过这项修复，您的驱动程序可以安全地组合在单个插针工厂中的 2D 和 3D 插针和 DirectSound 将正确地报告的 2D 和 3D pin 计数。 此外，当 DirectSound 需要 2D pin 时，它使用 3D 2D pin 代替 pin 仅当它已用尽 2D 插针从所有 pin 工厂提供。

 

 




