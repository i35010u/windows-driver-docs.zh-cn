---
title: 使用用户模式调试程序调试设备安装
description: 使用用户模式调试程序调试设备安装
ms.assetid: 34427afb-3303-44ec-a3a7-72f247c5506d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60b598798519d55b344f4f3da516dce81ac0ffc4
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095977"
---
# <a name="debugging-device-installations-with-a-user-mode-debugger"></a>使用用户模式调试程序调试设备安装


从 Windows Vista 开始，当即插即用 (PnP) manager 在系统中检测到新设备时，操作系统将启动设备安装主机进程 (*DrvInst.exe*) 搜索并安装设备驱动程序。

调试用户模式设备安装主机进程的最有效方法是使用用户模式调试器，如 WinDbg 或 Visual Studio。 由于 *DrvInst.exe* 进程通常在无需任何用户交互的情况下完成，因此 Microsoft 添加了对 windows Vista 和更高版本的 windows 的支持，以便在处理设备安装的核心阶段之前， [驱动程序包](driver-packages.md) 的开发人员能够附加调试器。

有关用户模式调试器和其他调试工具的详细信息，请参阅 [Windows 调试](../debugger/index.md)。

**DebugInstall**注册表值指定在系统上启用的设备安装调试支持的类型。 有关此注册表值的详细信息，请参阅 [启用对调试设备安装的支持](enabling-support-for-debugging-device-installations.md)。

如果将 **DebugInstall** 注册表值设置为2，则在继续安装之前， *DrvInst.exe* 将等待用户模式调试器附加到其进程。 附加调试器后，进程将中断调试器本身。 应附加和配置调试器，以便它不会在要调试的目标系统中启动自己的初始断点。

例如，调试程序可以按名称附加到 *DrvInst.exe* ：

```cpp
C:\>C:\Debuggers\WinDbg.exe -g -pn DrvInst.exe
```

或者，如果将调试器附加到目标系统，将显示以下调试信息：

```cpp
DRVINST.EXE: Waiting for debugger on Process ID = 3556 ......
```

这允许将调试器附加到 *DrvInst.exe* 进程，方法是使用其唯一的进程 ID：

```cpp
C:\>C:\Debuggers\WinDbg.exe -g -p 3556
```

将用户模式调试器附加到 *DrvInst.exe* 进程后，该进程将中断调试器：

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

由于尚未处理设备安装的核心阶段，因此尚未加载用于该设备的任何类安装程序或共同安装程序 Dll。

如果事先知道断点的模块和函数名称，则可以使用 "bu" 调试器命令将该名称设置为无法解析的断点。 下面的代码示例演示如何为 *MyCoinst.dll* 联安装程序 (CoInstallerProc) 的主入口点设置未解析的断点：

```cpp
0:000> bu mycoinst!CoInstallerProc
0:000> bl
 0 eu             0001 (0001) (mycoinst!CoInstallerProc)
```

当加载 *MyCoinst.dll* 联安装程序并到达断点时：

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

类安装程序或共同安装程序 DLL 不应预测何时将从 *DrvInst.exe* 进程中加载或卸载。 但是，即使卸载模块，使用 "bu" 设置的断点仍将保留。

或者，可以通过为该 DLL 的 load 事件设置调试器异常，来执行 *DrvInst.exe* 过程，以将特定的类安装程序或共同安装程序 DLL 加载到进程中：

```cpp
0:000> sxe ld mycoinst.dll
```

0:000 &gt; g

加载模块后，可以在 DLL 中设置断点。 例如：

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

由于断点已设置为未解析的断点 (bu) ，即使模块已卸载，它仍将保持设置。

完成安装过程的默认时间段为5分钟。 如果该进程未在给定的时间段内完成，系统会假定进程挂起 (停止响应) ，并且安装过程将终止。

如果在设备安装过程中将用户模式调试器附加到目标系统，则系统不会强制执行此超时期限。 这使得 [驱动程序包](driver-packages.md) 开发人员可以花费时间来调试安装过程。

 

