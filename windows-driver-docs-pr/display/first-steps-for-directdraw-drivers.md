---
title: 使用 DirectDraw 驱动程序的前几个步骤
description: 使用 DirectDraw 驱动程序的前几个步骤
keywords:
- 绘制 WDK DirectDraw，DirectDraw 驱动程序
- DirectDraw WDK Windows 2000 显示，DirectDraw 驱动程序
- DirectDraw driver WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af1e5be049ba809bb77a3bea058701d3fa1a2b8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783281"
---
# <a name="first-steps-for-directdraw-drivers"></a>使用 DirectDraw 驱动程序的前几个步骤


## <span id="ddk_first_steps_for_directdraw_drivers_gg"></span><span id="DDK_FIRST_STEPS_FOR_DIRECTDRAW_DRIVERS_GG"></span>


开始实现 DirectDraw 功能的一个好方法是修改现有的驱动程序。 如果没有可用的驱动程序，请从 Windows 驱动程序工具包的 DirectDraw 部分中的示例代码开始 (WDK) 并获取驱动程序初始化、锁定和翻转工作。 从该基本功能可以添加功能更强大的功能，以提高显示性能。

DirectDraw 的最小驱动程序功能需要能够锁定、解锁和翻转图面。 假设硬件支持相关操作，还应为 blts (添加驱动程序支持，包括透明 blts，这对) 游戏中的速度非常重要，因为这对于视频播放至关重要。

 

 





