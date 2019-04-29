---
title: 有关 DirectInput 控制面板
description: 有关 DirectInput 控制面板
ms.assetid: d6845778-1203-4b5a-8a7b-7d4eecbcc59e
keywords:
- 属性表 WDK DirectInput 有关控制面板
- 游戏控制器 WDK DirectInput 有关控制面板
- 有关控件面板控件面板 WDK DirectInput
- Joy.cpl
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25d058c55351bf8233cdd0d7a0f37cc07c6cff14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390403"
---
# <a name="about-the-directinput-control-panel"></a>有关 DirectInput 控制面板





DirectInput 游戏控制器，如游戏板、 游戏杆和强制反馈设备提供支持。 在 Microsoft DirectX 5.0 和更高版本中，DirectInput 提供名为 Joy.cpl 一个新游戏控制器控制面板。 此版本是控制面板的第一个允许可扩展性，为每个控制器显示属性表可以替换为特定于该控制器的属性页。 这是通过创建一个 DLL，它包含有关这些属性表的信息。 此 DLL 公开 DirectInput 控制面板到调用的 COM 接口。

游戏控制器硬件供应商不建议使用此扩展性功能为其游戏控制器而不是创建一个单独的控件面板提供自定义的属性表。 这允许用户打开单个控制面板来配置和测试其游戏控制器。

 

 




