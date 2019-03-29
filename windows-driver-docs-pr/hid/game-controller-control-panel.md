---
title: 游戏控制器控制面板
description: 游戏控制器控制面板
ms.assetid: fb68102a-24d6-4dda-8f27-69366a2129bc
keywords:
- 属性表 WDK DirectInput，控件面板结构
- 游戏控制器 WDK DirectInput，控件面板结构
- 控制面板 WDK DirectInput，体系结构
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1beb73c41d4b2f2e6cfc116a0b92077a39febb63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563636"
---
# <a name="game-controller-control-panel"></a>游戏控制器控制面板





DirectInput 控件面板的基本体系结构包含的 DirectInput 游戏控制器控件面板中，支持的抽象层库**IDIGameCntrlPropSheet** COM 接口，并为每个 COM 对象游戏控制器属性表。

**请注意**   "对象"一词描述 CreateInstance 来支持 COM 接口的方法，即使这些方法不通过一种编程语言面向对象的 c + + 等调用创建的实体。 "表"一词描述向其中插入页的对话框。 单词"page"描述"属性表"对话框的内容对话框。

 

Microsoft Windows 95/98/Me 和 Windows NT 4.0 及更高版本之间的可移植性，为了 DirectInput 控制面板可直接处理 DirectInput，又可直接与设备驱动程序。 作为此副产品，DirectInput 控件面板具有输入设备，即使在应用程序处于后台时的访问权限。

 

 




