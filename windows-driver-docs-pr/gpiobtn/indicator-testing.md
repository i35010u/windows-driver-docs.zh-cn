---
title: 指示器测试
description: 本主题介绍常见指示器步骤过程和示例。
ms.assetid: 8FD5728C-30E3-4998-A01D-80894BDB379A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ea28fcbc8e85286083521fe4cf00cb8ddd5747b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323278"
---
# <a name="indicator-testing"></a>指示器测试


本主题介绍常见指示器步骤过程和示例。

## <a name="span-idtouchkbdspanspan-idtouchkbdspantouch-keyboard-deployment-steps"></a><span id="touchkbd"></span><span id="TOUCHKBD"></span>触摸键盘部署步骤


以下步骤来测试是否触摸键盘打开自动 （而不是从任务栏打开它的用户）。 "执行触摸键盘部署步骤"的测试指示您每次应用的以下步骤。

1.  按 Windows 按钮以导航到**启动**。
2.  幻灯片以显示**超级按钮**菜单，然后选择**搜索**。
3.  点击编辑字段中。

## <a name="span-idconvspanspan-idconvspanslatelaptop-mode-conversion-steps"></a><span id="conv"></span><span id="CONV"></span>静态图像/便携式计算机模式转换步骤


将转换为静态图像 （或便携式计算机），如测试所指示。

**请注意**  如果系统可以使用多个方法转换到盖板模式，请对每个方法重复测试步骤。

各种外形规格允许的转换，如下所示的不同方法：

-   附加或分离键盘
-   翻转屏幕
-   可在屏幕旋转
-   若要覆盖或发现键盘将屏幕滑动

**转换示例：**

![键盘附加和分离的转换](images/keyboardattachdetachconvertible.jpg)

**图 1 键盘附加和分离转换**

![屏幕旋转转换](images/screenswivelconvertible.jpg)

**图 2 屏幕旋转转换**

 

**盖板示例：**

-   键盘分离
-   键盘键入轻松存在但不可访问
    -   键盘 flapped 下方
    -   下面的幻灯片
    -   Swivelled

**便携式计算机模式下：**

键盘是用于轻松键入存在并且可访问。

## <a name="span-idlaptopslatemodeindicatorscenariosspanspan-idlaptopslatemodeindicatorscenariosspanspan-idlaptopslatemodeindicatorscenariosspanlaptopslate-mode-indicator-scenarios"></a><span id="Laptop_slate_mode_indicator_scenarios"></span><span id="laptop_slate_mode_indicator_scenarios"></span><span id="LAPTOP_SLATE_MODE_INDICATOR_SCENARIOS"></span>便携式计算机/盖板模式指示器方案


请务必执行端到端测试双用型公开以下几个方面中的任何潜在问题的指示器：

-   将系统从一种模式转换为另一种模式时的各种计时。
-   可转换的机械具体信息。

 

 




