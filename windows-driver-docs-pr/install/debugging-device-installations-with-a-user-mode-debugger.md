---
title: 使用用户模式调试程序调试设备安装
description: 使用用户模式调试程序调试设备安装
ms.assetid: 34427afb-3303-44ec-a3a7-72f247c5506d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a86b65d148ce509e7e85619775ce7fadd8427728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358853"
---
# <a name="debugging-device-installations-with-a-user-mode-debugger"></a>使用用户模式调试程序调试设备安装


Windows vista 中，从开始，当插即用 (PnP) 管理器检测到系统中的新设备时，在操作系统启动设备安装主机进程 (*DrvInst.exe*) 若要搜索并安装设备的驱动程序。

调试用户模式设备安装主机进程的最有效方法是使用用户模式下调试程序，如 WinDbg 或 Visual Studio。 因为*DrvInst.exe*进程会正常情况下完成而无需任何用户交互、 Microsoft Windows Vista 和更高版本的 Windows，以允许开发人员添加了支持[驱动程序包](driver-packages.md)处理设备安装的核心阶段之前附加调试器。

有关用户模式调试程序和其他调试工具的详细信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

**DebugInstall**注册表值指定的调试支持系统启用的设备安装的类型。 有关此注册表值的详细信息，请参阅[启用支持调试设备安装](enabling-support-for-debugging-device-installations.md)。

当**DebugInstall**注册表值设置为 2， *DrvInst.exe*将等待用户模式的调试程序附加到其进程中，再继续安装。 附加调试器后，该过程将中断调试器本身。 应附加调试程序，并将其配置，以便它不会启动其自身初始断点正在调试的目标系统中。

例如，调试器可以附加到*DrvInst.exe*按名称：

```cpp
C:\>C:\Debuggers\WinDbg.exe -g -pn DrvInst.exe
```

或者，如果调试程序附加到目标系统中，将显示以下的调试信息：

```cpp
DRVINST.EXE: Waiting for debugger on Process ID = 3556 ......
```

这使调试器附加到*DrvInst.exe*进程通过其唯一的进程 ID:

```cpp
C:\>C:\Debuggers\WinDbg.exe -g -p 3556
```

在用户模式后调试程序附加到*DrvInst.exe*过程中，该过程将中断到调试器：

```cpp
Debugger detected!
DRVINST.EXE: Entering debugger during PnP device installation.
Device instance = "X\Y\Z" ...

(d48.5a0): Break instruction exception - code 80000003 (first chance)
eax=7ffde000 ebx=00000000 ecx=00000000 edx=77f745c0 esi=00000000 edi=00000000
eip=77f24584 esp=0105ff74 ebp=0105ffa0 iopl=0         nv up ei pl zr na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000246
ntdll!DbgBreakPoint:
77f24584 cc               int     3

0:000> |
.  0id: d48attachname: E:\Windows\system32\DrvInst.exe
```

因为尚未处理的设备安装的核心阶段，任何类安装程序或辅助安装程序的设备使用的 Dll 尚未加载。

如果针对某个断点的模块和函数名称事先已知的可以使用"bu"调试器命令为无法解析断点设置该名称。 下面的代码示例演示如何设置的主入口点 (CoInstallerProc) 无法解析的断点的*MyCoinst.dll*共同安装程序：

```cpp
0:000> bu mycoinst!CoInstallerProc
0:000> bl
 0 eu             0001 (0001) (mycoinst!CoInstallerProc)
```

当*MyCoinst.dll*共同安装程序已加载并且达到断点：

```cpp
Breakpoint 0 hit
eax=00000001 ebx=00000000 ecx=00000152 edx=00000151 esi=01a57298 edi=00000002
eip=5bcf54f1 esp=0007e204 ebp=0007e580 iopl=0         nv up ei pl nz na pe nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000202
mycoinst!CoInstallerProc:
5bcf54f1 8bff             mov edi,edi
0:000> bl
 0 e 5bcf54f1     0001 (0001)  0:**** mycoinst!CoInstallerProc
```

类安装程序或辅助安装程序 DLL，分别将会加载或卸载时从应不预测*DrvInst.exe*过程。 但是，即使在卸载模块，将保持使用"bu"设置断点。

或者， *DrvInst.exe*进程可能允许执行直到其中一个特定的类的安装程序或通过设置该 DLL 的调试程序异常的 load 事件中，共同安装程序 DLL 被加载到进程：

```cpp
0:000> sxe ld mycoinst.dll
```

0:000&gt; g

加载该模块后，可以在 DLL 内设置断点。 例如：

```cpp
ModLoad: 5bcf0000 5bd05000   C:\WINDOWS\system32\mycoinst.dll
eax=00000000 ebx=00000000 ecx=011b0000 edx=7c90eb94 esi=00000000 edi=00000000
eip=7c90eb94 esp=0007da54 ebp=0007db48 iopl=0         nv up ei ng nz ac po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000296
ntdll!KiFastSystemCallRet:
7c90eb94 c3               ret
0:000> .reload mycoinst.dll
0:000> x mycoinst!*InstallerProc*
5bcf54f1 mycoinst!CoInstallerProc (unsigned int, void *, struct _SP_DEVINFO_DATA *)

0:000> bu mycoinst!CoInstallerProc
0:000> bl
 0 e 3b0649d5     0001 (0001)  0:**** mycoinst!CoInstallerProc
0:000> sxd ld mycoinst.dll
0:000> g
Breakpoint 0 hit
eax=00000001 ebx=00000000 ecx=000001d4 edx=000001d3 esi=000bbac0 edi=00000002
eip=5bcf54f1 esp=0007e204 ebp=0007e580 iopl=0         nv up ei pl nz na pe nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000202
mycoinst!CoInstallerProc:
5bcf54f1 8bff             mov edi,edi
0:000> 
```

为无法解析的断点 (bu) 设置了断点，因为帐户会保留设置，即使在卸载模块。

默认值才能完成安装过程的时间段为 5 分钟。 如果在给定的时间段内未完成该过程，系统将认为进程挂起 （已停止响应），并且安装过程已被终止。

如果设备安装过程中将用户模式下调试程序附加到目标系统中，系统不会强制此超时时间。 这允许[驱动程序包](driver-packages.md)调试安装过程所需的开发人员需花费时间。

 

 





