---
title: 支持混合使用 2D 和 3D 引脚
description: 支持混合使用 2D 和 3D 引脚
keywords:
- 硬件加速 WDK DirectSound、二维和3D 引脚混合
- 3D 混合 WDK 音频
- 2D 混合 WDK 音频
- 固定 WDK 音频、2D
- 固定 WDK 音频，3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07594f60f4d41309264efa9fb577f28b2fe49d2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800581"
---
# <a name="supporting-a-mixture-of-2d-and-3d-pins"></a>支持混合使用 2D 和 3D 引脚


## <span id="supporting_a_mixture_of_2d_and_3d_pins"></span><span id="SUPPORTING_A_MIXTURE_OF_2D_AND_3D_PINS"></span>


如果 WDM 音频驱动程序支持二维和3D 插针，则可以将3D 插为双精度，以用作2D 旋转，反之亦然。 当 DirectSound 需要 2D pin 时，它可以将未使用的 3D pin 替换为该用途（如果驱动程序提供了一个）。 不过，如果 DirectSound 需要 3D pin，它会继续搜索驱动程序的 pin 实例列表，直到找到 3D pin，并忽略在搜索过程中遇到的任何2D 针。 DirectSound 按列出的顺序检查驱动程序的 pin 工厂列表，直到找到满足其要求的 pin 实例。

在报告 2D pin 计数时，驱动程序应指定2D 针实例的数量以及3D 插针实例的数目。 在报告 3D pin 计数时，驱动程序应忽略2D 引脚并仅指定3D 固定的实例数。

与 Microsoft Windows 2000 和 Windows 98 一起分发的 DirectSound 版本在处理公开二维和三维引脚混合的 pin 工厂时存在一个已知问题： DirectSound 将 3D pin 计数错误地报告为2D 引脚实例数加上3D 引脚实例数。 此问题的解决方法是编写驱动程序，使其将二维和3D 插分隔开来到两个不同的 pin 工厂。 一个工厂只公开2D 引脚，另一个工厂仅公开3D 引脚。

对于 WDM 驱动程序，DirectSound 会将二维 pin 计数正确地报告为两个工厂的2D 和3D 引脚的计数之和，并将 3D pin 计数正确地报告为一台3D 固定工厂中的 3D pin 数。 公开2D 和3D 引脚的单独工厂时，驱动程序应列出3D 固定工厂之前的2D 引脚工厂。 这是必需的，因为当 DirectSound 正在查找 2D pin 时，它将使用它找到的第一条2D 或3D 旋转，DirectSound 会按照驱动程序列出它们的顺序检查固定工厂。 如果驱动程序首先列出3D 工厂，则有 DirectSound 不必要地使用 3D pin 来取代2D 引脚，这会产生不必要的情况。

总之，如果驱动程序公开了二维和3D 插针，则应该遵循以下规则，以便在 DirectSound 的早期版本上正确运行：

-   分别为二维和3D 引脚提供两个单独的 pin 工厂。

-   列出3D 固定工厂前面的2D 引脚工厂。

这些解决方法在 DirectSound 的更高版本中是不必要的。 上面所述的问题在 Windows Me 和 Windows XP 及更高版本中已修复。 它还在 DirectSound 8 中得到了修复，该版本在早期版本的 Windows 版本中进行重新分发。 使用此修补程序，你的驱动程序可以安全地将二维和3D 引脚组合到一个插针工厂中，DirectSound 将正确报告2D 和3D 引脚计数。 此外，当 DirectSound 需要 2D pin 时，仅当它已用尽所有 pin 工厂提供的 2D pin 时，它才会使用 3D pin 来替代 2D pin。

 

 




