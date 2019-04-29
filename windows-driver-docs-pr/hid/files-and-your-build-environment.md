---
title: 文件和生成环境
description: 文件和生成环境
ms.assetid: 0c85a599-65bb-45e5-a2f8-eefd47e82025
keywords:
- 属性表 WDK DirectInput，文件
- 游戏控制器 WDK DirectInput，文件
- 控制面板 WDK DirectInput，文件
- 属性表 WDK DirectInput 构建环境
- 游戏控制器 WDK DirectInput，构建环境
- 控件面板 WDK DirectInput，构建环境
- 构建环境 WDK DirectInput
- 文件 WDK DirectInput
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5bcc177b9c3c78c2b0ff62f17445c0e4151baa0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388961"
---
# <a name="files-and-your-build-environment"></a>文件和生成环境





至少，您将需要直接 X 直接开发工具包 (DDK) 标头文件 Dicpl.h。 此文件向你提供所需的接口、 结构、 类定义和错误。 建议你使用的 DirectInput **IDirectInputJoyConfig8**可确保在属性表的所有注册表访问的接口也可在 Windows NT 4.0 及更高版本。 如果您计划在属性页中使用 DirectInput，您还必须使用关联的 DirectX SDK 文件。 DirectInput 控制面板中的所有结构都打包在 8 字节边界上。 验证属性表在 8 字节边界上封装结构。

**请注意**  时测试控制面板，请确保其主显示器设置为 640 x 480 像素的分辨率的系统上对其进行测试。 请确保所有控件都都减少解析时仍然可见。

 

 

 




