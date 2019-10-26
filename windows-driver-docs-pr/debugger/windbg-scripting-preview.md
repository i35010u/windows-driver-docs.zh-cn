---
title: WinDbg 预览-脚本菜单
description: 本部分介绍如何在 WinDbg 预览调试器中使用脚本。
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53e905612da91fc55e187f99d0d6d98df198452f
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916117"
---
# <a name="windbg-preview---scripting"></a>WinDbg 预览-脚本 

本部分介绍如何使用 WinDbg 预览版中的脚本支持。

![调试器中脚本菜单的屏幕截图](images/windbgx-javascript-new-script.png)

"WinDbg 预览脚本" 窗口功能基本语法突出显示、IntelliSense 和错误识别。 

使用功能区按钮可以：
- 创建新脚本 
- 打开现有脚本
- 执行脚本
- 保存脚本 
- 取消链接脚本
- 加载 JavaScript 提供程序

还可以通过在脚本窗口中右键单击并选择 *"保存时执行脚本"* 来自动执行脚本。 成功加载脚本后，会在脚本标题栏中显示一个绿色的复选框。 如果脚本中出现错误，则会显示一个红色的 x。

## <a name="javascript-scripting"></a>JavaScript 脚本编写 

若要开始使用 JavaScript，必须首先调试目标。 准备好开始处理 JavaScript 时，请单击 "加载 JavaScript 提供程序"。 之后，你可以通过在这两种类型的脚本模板之间进行选取，来创建新的 JavaScript。

- **扩展脚本**-旨在充当调试器扩展的脚本。  它操作调试器的对象模型，并提供持续功能。  在功能区上命中 "<i>执行</i>" 按钮不会执行任何操作。

- **命令性脚本**-一种脚本，每次在功能区上单击 "<i>执行</i>" 按钮时，该脚本都可执行操作。 此类脚本通常不会修改调试器的对象模型。

有关使用 JavaScript 的详细信息，请参阅以下主题：

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)

## <a name="natvis-scripting"></a>NatVis 脚本 

使用**新脚本** > **NatVis**打开以下空白 NatVis 模板。

```xml
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
  <Type Name="">
  </Type>
</AutoVisualizer>
```

有关使用 NatVis 的详细信息，请参阅[NatVis 中的调试器对象](native-debugger-objects-in-natvis.md)。

 
---

## <a name="see-also"></a>另请参阅

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
