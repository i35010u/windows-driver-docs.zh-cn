---
title: 使用 Windows 调试工具中提供的主题
description: 使用 Windows 调试工具中提供的主题
ms.assetid: d3571a7a-cdab-4a17-b4e0-ffb1690de642
keywords:
- 提供的主题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8469e0ad441e7f3c67763e4a5d9330f11c475aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390575"
---
# <a name="using-themes-provided-in-debugging-tools-for-windows"></a>使用 Windows 调试工具中提供的主题


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


本主题说明从四个主题中的 Windows 调试工具提供的每个配置的屏幕快照。 这些主题是 Standard.reg、 Standardvs.reg、 Srcdisassembly.reg 和 Multimon.reg。

### <a name="span-idstandardregspanspan-idstandardregspanstandardreg"></a><span id="standard_reg"></span><span id="STANDARD_REG"></span>Standard.reg

Standard.reg 主题可用于大多数调试目的。 在这种配置，WinDbg 窗口的较低的第三个均由调试器命令窗口。 上部的三分之二分为大约一半。 指示源窗口在其中打开选项卡式的集合中的占位符窗口的左半部分所占用。 右半部分又进一步分为部分垂直。 上半部分包含一个选项卡式的集合，其中包含监视、 局部变量、 寄存器和反汇编窗口。 下半部分包含一个选项卡式的集合，其中包括调用和进程和线程窗口。

在每个停靠位置的占位符窗口，还包含为在其他窗口的参考点。 占位符 windows 应不会关闭，因为将其关闭，则可能会更改 windows 的配置。 停靠所有的窗口中查看这种排列方式。下面的屏幕截图显示了 Standard.reg 主题。

![standard.reg 主题的屏幕截图](images/theme-standard.jpg)

### <a name="span-idstandardvsregspanspan-idstandardvsregspanstandardvsreg"></a><span id="standardvs_reg"></span><span id="STANDARDVS_REG"></span>Standardvs.reg

Standardvs.reg 主题可用于大多数调试情况下，但在布局中更类似于 Visual Studio。 在这种配置，WinDbg 窗口划分为水平折。 上面第三个又进一步分为垂直部分。 右上的左半部分第三个包含一个选项卡式的集合，其中包括监视、 局部变量、 寄存器、 内存、 反汇编、 和便签簿窗口。 上面的右半部分第三个包含一个选项卡式的集合，其中包括调用和进程和线程 windows。 WinDbg 窗口的较低的第三个均由调试器命令窗口。 第三个中间通过指示源窗口选项卡式的集合中的打开其中一个占位符窗口来填充。

在每个停靠位置的占位符窗口，还包含为在其他窗口的参考点。 占位符 windows 应不会关闭，因为将其关闭，则可能会更改 windows 的配置。 停靠所有的窗口中查看这种排列方式。 下面的屏幕截图显示了 Standardvs.reg 主题。

![standardvs.reg 主题的屏幕截图](images/theme-standardvs.jpg)

### <a name="span-idsrcdisassemblyregspanspan-idsrcdisassemblyregspansrcdisassemblyreg"></a><span id="srcdisassembly_reg"></span><span id="SRCDISASSEMBLY_REG"></span>Srcdisassembly.reg

Srcdisassembly.reg 主题包括一个反汇编窗口中的，在程序集模式中进行调试。 在这种配置，WinDbg 窗口分为两半竖向，和每个格式正确的后半部分进一步划分为三水平。 右半部分，右上第三个是局部变量选项卡式的集合和监视窗口，中间第三个调试器命令窗口中，，越低第三个选项卡式的进程、 线程和调用 windows 集合。 指示源窗口打开选项卡式的集合; 中的其中一个占位符窗口的左半部分，执行上部的三分之二越低第三个是占用反汇编窗口。

在每个停靠位置的占位符窗口，还包含为在其他窗口的参考点。 占位符 windows 应不会关闭，因为将其关闭，则可能会更改 windows 的配置。 停靠所有的窗口中查看这种排列方式。 下面的屏幕截图显示了 Srcdisassembly.reg 主题。

![srcdisassembly.reg 主题的屏幕截图](images/theme-srcdisassembly.jpg)

### <a name="span-idmultimonregspanspan-idmultimonregspanmultimonreg"></a><span id="multimon_reg"></span><span id="MULTIMON_REG"></span>Multimon.reg

使用多个监视器进行调试设置 Multimon.reg 主题。 在这种配置，创建新的停靠，因此 WinDbg 窗口可以查看一个监视器上，并可以在其他监视器上查看新的停靠。 指示源窗口在其中打开选项卡式的集合中的占位符窗口的情况下，WinDbg 窗口都会填满。 新的停靠分为 fourths。 左上角包含一个选项卡式的集合，其中包括监视和局部变量窗口。 右上角包含一个选项卡式的集合，其中包含寄存器、 内存、 反汇编、 便签簿，并且进程和线程窗口。 左下方包含调试器命令窗口。 右下方包含调用窗口。

在每个停靠位置的占位符窗口，还包含为在其他窗口的参考点。 占位符 windows 应不会关闭，因为将其关闭，则可能会更改 windows 的配置。 停靠所有的窗口中查看这种排列方式。 下面的屏幕截图显示了 Multimon.reg 主题。

![multimon.reg 主题的屏幕截图](images/theme-multimon.jpg)

 

 





