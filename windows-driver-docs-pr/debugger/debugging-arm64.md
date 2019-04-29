---
title: 调试 ARM64
description: 调试 ARM64
keywords:
- 调试 ARM64
- 调试
- ARM64
ms.date: 07/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: c22cbe5a780f1353c15b9c5dabde6e83e2d262dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377193"
---
# <a name="debugging-on-arm64"></a>在 ARM64 上进行调试

本主题介绍调试 ARM 处理器上的 Windows 10。 有关 ARM 上 Windows 10 的常规信息，请参阅[ARM64 上的 Windows 10 桌面版](https://docs.microsoft.com/windows/uwp/porting/apps-on-arm)。

一般情况下，调试用户模式应用程序的开发人员应使用的调试程序与目标应用程序体系结构匹配的版本。 使用 WinDbg 的 ARM64 版本来调试用户模式 ARM64 应用程序并使用 ARM 版本的 WinDbg 调试用户模式 ARM32 应用程序。 使用 x86 版本的 WinDbg 调试 ARM64 的处理器上运行的用户模式 x86 应用程序。  

在极少数情况下需要调试系统代码 – 例如 WOW64 或 CHPE – 可以使用 WinDbg 的 ARM64 版本。 如果你正在调试 ARM64 内核将从另一台计算机，使用 WinDbg 这台计算机的体系结构匹配的版本。  


## <a name="getting-arm--debugging-tools-for-windows"></a>获取 ARM Windows 调试工具 

你可以获取的调试工具用于 ARM64 下载[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) (版本 10.0.16299 或更高版本)。  安装过程中，选择*有关 Windows 调试工具*框。 

调试工具位于`Debuggers`工具包安装目录中的文件夹。  工具是在 x86 `Debuggers\x86`，ARM32 工具正在`Debuggers\ARM`，和 ARM64 工具都在之下`Debuggers\ARM64`。 

## <a name="debugging-arm64-code"></a>调试 ARM64 代码

所需 ARM64 WinDbg ARM64 的代码进行调试。 调试体验是类似于调试 x86 应用程序具有 x86 WinDbg 在 x86 Windows，但以下差异除外。 

- 有 32 通用寄存器-x0 到 x28 和 fp，lr，sp。 
- 程序计数器寄存器的 pc，不是常规用途注册。 
- 所有通用都寄存器和 pc 寄存器都是 64 位的宽度。 
- 最多 2 个活动的数据断点执行和读/写内存的 2 个活动的数据断点。 有关详细信息，请参阅[处理器断点](https://docs.microsoft.com/windows-hardware/drivers/debugger/processor-breakpoints---ba-breakpoints-)。 


## <a name="debugging-x86-user-mode-code"></a>调试 x86 用户模式代码 

在极少数情况下，您需要使用 ARM64 WinDbg 调试将 x86 用户模式代码，您可以使用以下 WinDbg 命令以上下文之间进行切换： 

- .effmach x86:切换到和 x86，请参阅上下文，模拟使用 x86 的效果 WinDbg。 
- .effmach arm64:切换到，请参阅 ARM64 上下文 
- .effmach chpe:切换到，请参阅 CHPE 上下文。 

有关.effmach 详细信息，请参阅[.effmach （有效的机器）](-effmach--effective-machine-.md)。

当调试 x86 应用程序在用户模式下，无论哪个 WinDbg 版本使用的，应注意这些事项。

- 如果没有被主动调试线程 （例如单单步执行、 遇到断点），未报告异常，且不在系统调用，寄存器上下文不能保持最新状态。 
- 在仿真程序在内部生成数据未对齐、 非法指令，在页 I/O 错误异常，并处理它生成的。 当使用 WinDbg 时，请考虑配置这些异常作为*忽略*下调试 / 事件筛选器... 菜单项。  
- 如果在用户模式下使用 ARM64 WinDbg，则不支持单步执行跨 x86 和 CHPE 函数边界。 若要解决此问题，请在目标代码上设置断点。 

有关支持 ARM64 和 WOW64 的常规信息，请参阅[运行 32 位应用程序](https://msdn.microsoft.com/library/windows/desktop/aa384249.aspx)64 位 Windows 编程指南中。 

有关调试在 WOW64 下运行的应用程序的信息，请参阅[调试 WOW64](https://msdn.microsoft.com/library/windows/desktop/aa384163.aspx)。



## <a name="debugging-in-visual-studio"></a>在 Visual Studio 中调试 

有关调试 ARM Visual Studio 中的信息，请参阅[远程调试](https://docs.microsoft.com/visualstudio/debugger/remote-debugging)。



## <a name="see-also"></a>请参阅

[使用 WDK 构建 ARM64 驱动程序](../develop/building-arm64-drivers.md)

[Windows 社区站立会议讨论始终连接电脑](https://blogs.windows.com/buildingapps/2018/01/22/windows-community-standup-discussing-always-connected-pc/)

-------






