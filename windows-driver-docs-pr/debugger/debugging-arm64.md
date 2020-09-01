---
title: 调试 ARM64
description: 调试 ARM64
keywords:
- 调试 ARM64
- 调试
- ARM64
ms.date: 07/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 42c0e553413226cb73a5366217cb29dd7ec013e9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209376"
---
# <a name="debugging-on-arm64"></a>在 ARM64 上进行调试

本主题介绍了如何调试 ARM 处理器上的 Windows 10。 有关 ARM 上的 Windows 10 的常规信息，请参阅 [ARM64 上的 windows 10 桌面](/windows/uwp/porting/apps-on-arm)。

通常，开发人员调试用户模式应用程序应使用与目标应用程序的体系结构相匹配的调试器版本。 使用 ARM64 版本的 WinDbg 调试用户模式 ARM64 应用程序，并使用此版本的 WinDbg 调试用户模式 ARM32 应用程序。 使用 WinDbg 的 x86 版本来调试在 ARM64 处理器上运行的用户模式 x86 应用程序。  

在需要调试系统代码的罕见情况下（如 WOW64 或 CHPE），可以使用 WinDbg 的 ARM64 版本。 如果要从另一台计算机调试 ARM64 内核，请使用与该其他计算机的体系结构匹配的 WinDbg 版本。  


## <a name="getting-arm--debugging-tools-for-windows"></a>获取适用于 Windows 的 ARM 调试工具 

可以通过下载 [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) (版本10.0.16299 或更高版本) 来获取用于 ARM64 的调试工具。  在安装过程中，选择 " *适用于 Windows 的调试工具* " 框。 

调试工具位于 `Debuggers` 工具包安装目录中的文件夹中。  X86 工具位于下 `Debuggers\x86` ，ARM32 工具位于下 `Debuggers\ARM` ，ARM64 工具在下 `Debuggers\ARM64` 。 

## <a name="debugging-arm64-code"></a>调试 ARM64 代码

调试 ARM64 代码需要 ARM64 WinDbg。 调试体验类似于在 x86 Windows 上用 x86 WinDbg 调试 x86 应用程序，但以下差异除外。 

- 有32个常规用途寄存器-从到 x28 和 fp，lr，sp 的 x0。 
- 程序计数器注册是一个常规用途的注册。 
- 所有常规用途寄存器和 pc 寄存器宽度均为64位。 
- 最多2个活动数据断点用于执行，2个活动数据断点用于读/写内存。 有关详细信息，请参阅 [处理器断点](./processor-breakpoints---ba-breakpoints-.md)。 


## <a name="debugging-x86-user-mode-code"></a>调试 x86 用户模式代码 

在极少数情况下，你需要使用 ARM64 WinDbg 调试你的 x86 用户模式代码，你可以使用以下 WinDbg 命令在上下文之间进行切换： 

- . effmach x86：切换到并参阅 x86 上下文，模拟使用 x86 WinDbg 的效果。 
- . effmach arm64：切换到并查看 ARM64 上下文 
- . effmach chpe：切换到并查看 CHPE 上下文。 

有关 effmach 的详细信息，请参阅 [effmach (有效的计算机) ](-effmach--effective-machine-.md)。

在用户模式下调试 x86 应用时，无论使用哪种 WinDbg 版本，都应注意这些注意事项。

- 如果未积极调试某个线程 (例如单步，遇到) 的断点，不报告异常，而不是在系统调用中，则寄存器上下文可能不是最新的。 
- 仿真器在内部生成未对齐的数据、非法的指令、页面内 i/o 错误异常，并处理它生成的错误。 使用 WinDbg 时，请考虑在调试/事件筛选器下将这些异常配置为 "已 *忽略* ..." 菜单项来访问更新。  
- 如果在用户模式下使用 ARM64 WinDbg，则不支持跨 x86 & CHPE 函数边界的单步执行。 若要解决此情况，请在目标代码上设置断点。 

有关 ARM64 和 WOW64 的一般信息，请参阅64位 Windows 编程指南中的 [运行32位应用程序](/windows/desktop/WinProg64/running-32-bit-applications) 。 

有关调试在 WOW64 下运行的应用程序的信息，请参阅 [调试 wow64](/windows/desktop/WinProg64/debugging-wow64)。



## <a name="debugging-in-visual-studio"></a>在 Visual Studio 中进行调试 

有关在 Visual Studio 中调试 ARM 的信息，请参阅 [远程调试](/visualstudio/debugger/remote-debugging)。



## <a name="see-also"></a>另请参阅

[使用 WDK 生成 ARM64 驱动程序](../develop/building-arm64-drivers.md)

[Windows 社区 Standup 讨论 Always 连接的 PC](https://blogs.windows.com/buildingapps/2018/01/22/windows-community-standup-discussing-always-connected-pc/)

-------