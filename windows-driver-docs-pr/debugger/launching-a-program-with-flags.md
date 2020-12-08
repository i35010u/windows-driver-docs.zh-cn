---
title: 启动带标志的程序
description: 启动带标志的程序
keywords:
- GFlags，启动带有标志的程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82faccd83ff105258acc8a3c6701ef10796e4024
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806535"
---
# <a name="launching-a-program-with-flags"></a>启动带标志的程序


## <span id="ddk_launching_a_program_with_flags_dtools"></span><span id="DDK_LAUNCHING_A_PROGRAM_WITH_FLAGS_DTOOLS"></span>


此功能使用指定标志运行一次程序。 这些设置仅影响启动的程序的实例。 它们不会保存在注册表中。

**启动带有标志的程序**

1.  单击 " **图像文件** " 选项卡。

2.  在 " **映像包** " 框中，键入可执行文件或 DLL 的名称，包括文件扩展名和程序的任何命令，然后按 tab 键。

    这会激活 " **启动** " 按钮和 " **图像文件** " 选项卡上的复选框。

3.  通过选中或清除与标志关联的复选框来设置或清除标志。

4.  单击 " **启动** " 按钮。

    以下屏幕截图显示 Windows Vista 中 "**图像文件**" 选项卡上的 "**启动**" 按钮。

    ![windows vista 中 "图像文件" 选项卡的屏幕截图 ](images/gflags-launch.png)

**注意**   注册表中设置的标志不会影响启动的程序的实例。
对话框中的标志集用于已启动的实例，即使它们不是图像文件标志也是如此。

 

 

 





