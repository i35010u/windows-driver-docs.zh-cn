---
title: 使用 Windows 调试工具中提供的主题
description: 使用 Windows 调试工具中提供的主题
keywords:
- 主题，已提供
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70d84291fd5b4fbbb6c5836dc9daa2b99e39f8e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803023"
---
# <a name="using-themes-provided-in-debugging-tools-for-windows"></a>使用 Windows 调试工具中提供的主题


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


本主题介绍 Windows 调试工具中提供的四个主题中的每个配置的屏幕截图。 这些主题为标准 .reg、Standardvs、Srcdisassembly 和 Multimon。

### <a name="span-idstandard_regspanspan-idstandard_regspanstandardreg"></a><span id="standard_reg"></span><span id="STANDARD_REG"></span>标准 .reg

标准 .reg 主题可用于大多数调试目的。 在这种排列中，将由调试器命令窗口来执行 WinDbg 窗口的第三方。 上部三分之二除以半部分。 左半部分由占位符窗口占用，后者指示源窗口在选项卡式集合中的打开位置。 右半部分将进一步分为半部分。 上半部分包含一个选项卡式集合，其中包含 "监视"、"局部变量"、"寄存器" 和 "反汇编" 窗口。 下半部分包含选项卡式集合，其中包括调用和进程和线程窗口。

在每个停靠位置，还包含一个占位符窗口作为其他窗口的引用点。 占位符窗口不应关闭，因为关闭它们可能会更改 windows 的配置。 此排列中的所有窗口都是固定的。下面的屏幕截图显示了标准 .reg 主题。

![标准 .reg 主题的屏幕截图](images/theme-standard.jpg)

### <a name="span-idstandardvs_regspanspan-idstandardvs_regspanstandardvsreg"></a><span id="standardvs_reg"></span><span id="STANDARDVS_REG"></span>Standardvs

Standardvs 主题可用于大多数调试目的，但更类似于布局到 Visual Studio。 在这种排列中，WinDbg 窗口水平分为三分之二。 将上半部分进一步划分为半部分。 上半部分的左半部分包含一个选项卡式集合，其中包括监视、局部变量、寄存器、内存、反汇编和便笺簿窗口。 上半部分的右半部分包含一个选项卡式集合，其中包括调用和进程和线程窗口。 WinDbg 窗口的第三个部分由调试器命令窗口执行。 中间的第三个由占位符窗口填充，后者指示在选项卡式集合中打开源窗口的位置。

在每个停靠位置，还包含一个占位符窗口作为其他窗口的引用点。 占位符窗口不应关闭，因为关闭它们可能会更改 windows 的配置。 此排列中的所有窗口都是固定的。 以下屏幕截图显示了 Standardvs 主题。

![standardvs 主题的屏幕截图](images/theme-standardvs.jpg)

### <a name="span-idsrcdisassembly_regspanspan-idsrcdisassembly_regspansrcdisassemblyreg"></a><span id="srcdisassembly_reg"></span><span id="SRCDISASSEMBLY_REG"></span>Srcdisassembly

Srcdisassembly 主题包含一个 "反汇编" 窗口，用于在程序集模式下进行调试。 在这种排列中，WinDbg 窗口以半角分为半角，而每一半形成的都是以水平方式划分为三分之二。 在右半部分，第三个是 "局部变量" 和 "监视" 窗口的选项卡式集合，中间第三个是调试器命令窗口，下半部分是进程和线程的选项卡式集合并调用窗口。 在左半部分，用一个占位符窗口来表示上三分之二，该窗口指示源窗口在选项卡式集合中的打开位置;第三个是 "反汇编" 窗口。

在每个停靠位置，还包含一个占位符窗口作为其他窗口的引用点。 占位符窗口不应关闭，因为关闭它们可能会更改 windows 的配置。 此排列中的所有窗口都是固定的。 以下屏幕截图显示了 Srcdisassembly 主题。

![srcdisassembly 主题的屏幕截图](images/theme-srcdisassembly.jpg)

### <a name="span-idmultimon_regspanspan-idmultimon_regspanmultimonreg"></a><span id="multimon_reg"></span><span id="MULTIMON_REG"></span>Multimon

Multimon 主题设置为可通过多个监视器进行调试。 在这种排列中，将创建一个新的停靠，以便可以在一个监视器上查看 WinDbg 窗口，并可以在另一个监视器上查看新的停靠。 WinDbg 窗口由占位符窗口填充，该窗口指示在选项卡式集合中打开源窗口的位置。 新的停靠划分为四分之三。 左上方包含一个选项卡式集合，其中包含 "监视" 和 "局部变量" 窗口。 右上方包含一个选项卡式集合，其中包括寄存器、内存、反汇编、便笺簿、进程和线程窗口。 左下方包含调试器命令窗口。 右下方包含 "调用" 窗口。

在每个停靠位置，还包含一个占位符窗口作为其他窗口的引用点。 占位符窗口不应关闭，因为关闭它们可能会更改 windows 的配置。 此排列中的所有窗口都是固定的。 以下屏幕截图显示了 Multimon 主题。

![multimon 主题的屏幕截图](images/theme-multimon.jpg)

 

 





