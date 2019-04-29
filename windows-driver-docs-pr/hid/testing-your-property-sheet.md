---
title: 测试属性表
description: 测试属性表
ms.assetid: 9886a758-392b-451d-874d-5ffcc5f9f5cd
keywords:
- 属性表 WDK DirectInput 测试
- 游戏控制器 WDK DirectInput，属性表测试
- 控件面板 WDK DirectInput 属性表测试
- 测试属性表 WDK DirectInput
- 调试控制面板应用程序 WDK DirectInput
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f8d4af0e5af9d0b1884d01277fcaf1980bec0e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384359"
---
# <a name="testing-your-property-sheet"></a>测试属性表





强烈建议您在属性表页在测试过程运行 DirectInput 和 DirectInput 控制面板的调试版本。 DirectX 组件设计用于调试窗口/终端发出有用的错误和警告消息。

调试控制面板应用程序可能很棘手。 使用以下步骤来调试自定义属性表页在 Microsoft 开发人员 Studio 5.0 及更高版本 （其他编译器具有类似的行为）。

1.  从**项目**菜单中，选择**设置**。

2.  选择**调试**选项卡。

3.  对于调试会话的可执行文件，输入 c:\\WINDOWS\\RUNDLL32。EXE (假设 c:\\WINDOWS 是 Windows 95/98/我目录) 如果在运行 Windows 95/98/我，或 c:\\WINNT\\SYSTEM32\\RUNDLL32。EXE (假设 c:\\WINNT 是操作系统目录) 如果你在运行 Windows NT 4.0 或更高版本。

4.  程序参数中，输入**shell32.dll,Control\_RunDLL c:\\windows\\系统\\joy.cpl**。 再次重申，这假定 c:\\WINDOWS 是你的 Windows 目录。 它是区分大小写，并且必须严格按照所示输入。

完成后，设置您的断点，并从生成菜单中，选择**开始调试**，然后**转**。 现在您就可以调试自定义属性表页。

 

 




