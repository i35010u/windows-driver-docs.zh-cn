---
title: 在调试器中运行程序
description: 在调试器中运行程序
keywords:
- GFlags，在调试器中运行程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e2c3aa61dc3a3417eb106bae18ca83270efc0c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786955"
---
# <a name="running-a-program-in-a-debugger"></a>在调试器中运行程序


## <span id="ddk_running_a_program_in_a_debugger_dtools"></span><span id="DDK_RUNNING_A_PROGRAM_IN_A_DEBUGGER_DTOOLS"></span>


此功能配置程序，以便它始终在具有指定选项的调试器中运行。 此设置保存在注册表中。 它会影响程序的所有新实例，并在更改前保持有效。

**在调试器中运行程序**

1.  单击 " **图像文件** " 选项卡。

2.  在 " **映像包** " 框中，键入可执行文件或 DLL 的名称（包括文件扩展名），然后按 tab 键。

    这会激活 " **图像文件** " 选项卡上的复选框。

3.  单击 " **调试器** " 复选框以将其选中。

    下面的屏幕截图显示 Windows Vista 中 "**映像文件**" 选项卡上的 "**调试器**" 复选框。

    ![windows vista 中 "映像文件" 选项卡上的 "调试器" 复选框屏幕截图 ](images/gflags-debugger.png)

4.  在 " **调试器** " 框中，键入运行调试器的命令，包括 (可选的路径) 和调试器和参数的名称。 例如， **ntsd-d-g-g x** 或 **c： \\ 调试器 \\cdb.exe-g-g**。

5.  单击“应用” 。

 

 





