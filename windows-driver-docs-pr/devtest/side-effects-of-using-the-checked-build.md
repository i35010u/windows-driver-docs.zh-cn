---
title: 使用已检验的版本的负面影响
description: 使用已检验的版本的负面影响
ms.assetid: 8c08d4f3-1221-4858-afd4-249d966c14a7
keywords:
- 检查内部版本号 WDK，对性能的影响
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143270b884efea157d98b35c3c50d6e9e7fc3205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534423"
---
# <a name="side-effects-of-using-the-checked-build"></a>使用已检验的版本的负面影响


## <span id="ddk_side_effects_of_using_the_checked_build_tools"></span><span id="DDK_SIDE_EFFECTS_OF_USING_THE_CHECKED_BUILD_TOOLS"></span>


检查的操作系统的组件包含较少的优化和更多的调试检查，比完全相同的免费组件。 因此，检查的组件的运行速度明显慢于免费对应项。

非常重要的驱动程序编写人员要记住，此执行速度变慢可能会导致更改代码路径之间的计时关系。 因此，调试内部版本可以隐藏在免费版本中可能会透露的计时问题 （如争用条件或死锁）。 因此，您必须测试所有免费生成和发布之前的操作系统的已检验的版本驱动程序。

 

 





