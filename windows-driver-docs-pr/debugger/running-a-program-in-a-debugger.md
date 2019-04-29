---
title: 在调试器中运行程序
description: 在调试器中运行程序
ms.assetid: e34b9560-33a2-47ed-83eb-84712b65a7f0
keywords:
- GFlags、 在调试器中运行的程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59f2c31404bf960eaf6bf2110aa5bad874f33a00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382064"
---
# <a name="running-a-program-in-a-debugger"></a>在调试器中运行程序


## <span id="ddk_running_a_program_in_a_debugger_dtools"></span><span id="DDK_RUNNING_A_PROGRAM_IN_A_DEBUGGER_DTOOLS"></span>


此功能，以便它始终在调试器中指定的选项中运行配置程序。 此设置保存在注册表中。 它会影响程序的所有新实例，并在更改之前保持有效。

**若要在调试器中运行程序**

1.  单击**映像文件**选项卡。

2.  在中**图像**框中，键入可执行文件或 DLL，其中包括文件扩展名的名称，然后按 TAB 键。

    这将激活上对应的复选框**映像文件**选项卡。

3.  单击**调试器**复选框以将其选中。

    下面的屏幕截图所示**调试器**上的复选框**图像文件**Windows Vista 中的选项卡。

    ![windows vista 中的图像文件选项卡上的调试器复选框的屏幕截图 ](images/gflags-debugger.png)

4.  在中**调试器**框中，键入要运行调试器，包括路径 （可选） 的命令和调试器和参数的名称。 例如， **ntsd-d-g-G-x**或**c:\\调试器\\cdb.exe-g-G**。

5.  单击 **“应用”**。

 

 





