---
title: 指示器测试
description: 本主题介绍常见的指标步骤步骤和示例。
ms.assetid: 8FD5728C-30E3-4998-A01D-80894BDB379A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ea28fcbc8e85286083521fe4cf00cb8ddd5747b
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242914"
---
# <a name="indicator-testing"></a>指示器测试


本主题介绍常见的指标步骤步骤和示例。

## <a name="span-idtouchkbdspanspan-idtouchkbdspantouch-keyboard-deployment-steps"></a><span id="touchkbd"></span><span id="TOUCHKBD"></span>触摸键盘部署步骤


以下步骤测试触摸键盘是否自动打开（与从任务栏打开它的用户相对）。 每次测试指示 "执行触控键盘部署步骤" 时，请应用以下步骤。

1.  按下 "Windows" 按钮，导航到 "**开始**"。
2.  滑动以显示 "**超级按钮**" 菜单，然后选择 "**搜索**"。
3.  在编辑字段中点击。

## <a name="span-idconvspanspan-idconvspanslatelaptop-mode-conversion-steps"></a><span id="conv"></span><span id="CONV"></span>石板/便携式计算机模式转换步骤


根据测试的指示，转换为石板（或便携式计算机）。

**请注意**   如果系统可以使用多种方法转换为石板模式，请对每个方法重复测试步骤。

各种外形规格允许不同的转换方法，例如：

-   附加或分离键盘
-   翻转屏幕
-   旋转屏幕
-   滑动屏幕以覆盖或揭开键盘

**转换示例：**

![用于转换的键盘附加和分离](images/keyboardattachdetachconvertible.jpg)

**图1键盘附加和分离转换**

![屏幕旋转转换](images/screenswivelconvertible.jpg)

**图2屏幕旋转转换**

 

**石板示例：**

-   已分离键盘
-   键盘存在，但无法轻松键入
    -   下的键盘 flapped
    -   下滑
    -   Swivelled

**笔记本电脑模式：**

键盘存在，可轻松键入。

## <a name="span-idlaptop_slate_mode_indicator_scenariosspanspan-idlaptop_slate_mode_indicator_scenariosspanspan-idlaptop_slate_mode_indicator_scenariosspanlaptopslate-mode-indicator-scenarios"></a><span id="Laptop_slate_mode_indicator_scenarios"></span><span id="laptop_slate_mode_indicator_scenarios"></span><span id="LAPTOP_SLATE_MODE_INDICATOR_SCENARIOS"></span>笔记本电脑/石板模式指示器方案


必须对改装执行端到端指示器测试，才能在以下领域公开任何潜在问题：

-   将系统从一种模式转换到另一种模式时的各种计时。
-   可转换的机械细节。

 

 




