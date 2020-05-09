---
title: 已检验版本的负面影响
description: 已检验版本的负面影响
ms.assetid: 8c08d4f3-1221-4858-afd4-249d966c14a7
keywords:
- 检查生成 WDK，性能影响
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 49c089d1928d37c2973fc3d147f441bd37bb116a
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999078"
---
# <a name="side-effects-of-using-the-checked-build"></a>已检验版本的负面影响

## <span id="ddk_side_effects_of_using_the_checked_build_tools"></span><span id="DDK_SIDE_EFFECTS_OF_USING_THE_CHECKED_BUILD_TOOLS"></span>

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

操作系统的选中组件包含的优化和调试检查比其他完全相同的可用组件更少。 因此，所选组件的运行速度远远低于可用的组件。

驱动程序编写器必须记住，这一较慢的执行可能会导致代码路径间的计时关系发生变化。 因此，选中的生成可以隐藏可能在免费生成中显示的计时问题（如争用条件或死锁）。 因此，在发布之前，必须在操作系统的免费版本和已检查内部版本上测试所有驱动程序。

 

 





