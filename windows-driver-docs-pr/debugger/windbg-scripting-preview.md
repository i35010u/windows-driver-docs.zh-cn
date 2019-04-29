---
title: WinDbg 预览版-脚本菜单
description: 本部分介绍如何使用 WinDbg 预览调试器中的脚本。
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45b2b80bf9d3514ca9bdc11a0d8c657518791c16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353059"
---
# <a name="windbg-preview---scripting"></a>WinDbg Preview - Scripting 

本部分介绍如何在 WinDbg 预览版中使用脚本的支持。

![在调试器中的脚本编写菜单的屏幕截图](images/windbgx-javascript-new-script.png)

WinDbg 预览脚本窗口功能基本语法突出显示、 IntelliSense 和错误识别。 

使用到功能区按钮：
- 创建新的脚本 
- 打开现有的脚本
- 执行脚本
- 保存脚本 
- 取消链接脚本
- 加载的 JavaScript 提供程序

您可以通过在脚本窗口中右键单击并选择也会自动执行脚本*执行脚本在保存*。 当您已成功加载脚本时，绿色的复选框将显示在脚本标题栏上。 如果在脚本中有错误，将显示一个红色的 x。

## <a name="javascript-scripting"></a>JavaScript 脚本 

若要开始使用 JavaScript，必须为调试目标。 如果你已准备好开始使用 JavaScript，单击"加载 JavaScript 提供程序"。 之后，您可以通过选取这些两种类型的脚本模板创建的新 JavaScript。

- **扩展脚本**-它旨在充当到调试器扩展的脚本。  其操作的对象模型的调试器，并提供持续的功能。  没有操作发生时达到<i>Execute</i>功能区上的按钮。

- **命令性脚本**-一个脚本，用于执行操作每次<i>Execute</i>功能区上单击按钮。 此类脚本通常不修改的对象模型的调试器。

有关使用 JavaScript 的详细信息，请参阅以下主题：

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[中 JavaScript 扩展本机调试器对象](native-objects-in-javascript-extensions.md)

[JavaScript 调试器的示例脚本](javascript-debugger-example-scripts.md)

## <a name="natvis-scripting"></a>NatVis 脚本 

使用**新的脚本** > **NatVis**打开以下空白 NatVis 模板。

```xml
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
  <Type Name="">
  </Type>
</AutoVisualizer>
```

有关使用 NatVis 的详细信息，请参阅[NatVis 调试器对象](native-debugger-objects-in-natvis.md)。

 
---

## <a name="see-also"></a>请参阅

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)

 





