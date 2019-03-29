---
title: 使用内核调试程序 (KD) 调试设备安装
description: 使用内核调试程序 (KD) 调试设备安装
ms.assetid: 0967d375-2602-44d2-b4ac-8d1e112afc3f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67a236e3391cae97bd201fe6f6d8790b2a4a4923
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567135"
---
# <a name="debugging-device-installations-with-the-kernel-debugger-kd"></a>使用内核调试程序 (KD) 调试设备安装


Windows vista 中，从开始，当插即用 (PnP) 管理器检测到系统中的新设备时，在操作系统启动设备安装主机进程 (*DrvInst.exe*) 若要搜索并安装设备的驱动程序。

此用户模式进程中发生设备安装，因为它是通常是最简单使用用户模式下调试程序，如中所述[使用用户模式下调试程序调试设备安装](debugging-device-installations-with-a-user-mode-debugger.md)。 在某些情况下，但是，可能会有帮助，以使用内核调试程序 (KD) 来监视用户模式下的设备安装过程。

例如，通过调试用户模式设备安装时使用 KD，可以执行以下操作：

-   同时使用调试内核模式问题 ！ devnode，！ devobj，！ drvobj，！ irp，和其他 KD 扩展。

-   监视的其他用户模式进程，而无需管理多个调试器使用 KD 扩展 ！ 进程或.process/p。

有关 KD 和其他调试工具的详细信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

**DebugInstall**注册表值指定的调试支持系统上启用的设备安装的类型。 有关此注册表值的详细信息，请参阅[启用支持调试设备安装](enabling-support-for-debugging-device-installations.md)。

当**DebugInstall**注册表值设置为 1， *DrvInst.exe*内核调试程序是已启用并且当前附加到调试器中断前将首先检查。 进行此中断后，可以在当前进程的用户模式模块中设置断点。 例如：

```cpp
kd> .reload /user
kd> bp /p @$proc setupapi!SetupDiCallClassInstaller
```

这将设置一个断点上例程 SETUPAPI ！当前进程 SetupDiCallClassInstaller。

为开发人员[驱动程序包](driver-packages.md)，通常最需要在设备的安装过程中调试类安装程序或辅助安装程序 DLL 的操作。 但是，当*DrvInst.exe*中断到调试器、 任何类安装程序或从驱动程序包的共同安装程序 Dll 将不加载。 尽管用户模式下调试程序支持以用户模式模块加载到进程时设置调试器异常"sx e ld"命令时，内核调试程序仅支持使用该命令的内核模式模块。

下面的代码示例演示如何"调试器命令程序"监视的特定类安装程序或辅助安装程序在当前进程中加载。 在此示例中，调试器命令程序将设置一个断点的主入口点 (CoInstallerProc) 上的*Mycoinst.dll*共同安装程序：

```cpp
file: Z:\bpcoinst.txt

r $t1 = 0
!for_each_module .if ($spat("@#ModuleName", "mycoinst*") = 0) {r $t1 = 1}
.if (not @$t1 = 0) {.echo mycoinst is loaded, set bp on mycoinst!CoInstallerProc } .else {.echo mycoinst not loaded}
.if (not @$t1 = 0) {.reload mycoinst.dll}
.if (not @$t1 = 0) {bp[0x20] /p @$proc mycoinst!CoInstallerProc } .else {bc[0x20]}
```

调试器命令程序执行时，将检查模块加载到当前进程的列表*Mycoinst.dll*。 之后此共同安装程序中加载 DLL，调试器将 CoInstallerProc 入口点函数上设置断点 （具有已知的断点 ID)。

由从调试中断开始启动*DrvInst.exe*主机进程中，您应首先上设置断点调用的返回地址位置*DrvInst.exe*内核调试器中分解。 此断点将清除所有设备安装过程中设置断点，并继续执行：

```cpp
DRVINST.EXE: Entering debugger during PnP device installation.
Device instance = "X\Y\Z" ...

Break instruction exception - code 80000003 (first chance)
010117b7 cc               int     3

kd> bp[0x13] /p @$proc @$ra "bc *;g"
```

接下来，应设置以允许在要在适当的时间在设备安装过程中执行的调试器命令程序的命令在进程内的某些断点。

若要确保该函数调用的设备安装之前设置类安装程序或辅助安装程序 DLL 入口点的断点，调试器命令程序应执行新 DLL 加载到当前进程中，也就是说，只要之后调用 LoadLibraryExW 返回：

```cpp
kd> .reload
kd> bp[0x10] /p @$proc kernel32!LoadLibraryExW "gu;$$><Z:\\bpcoinst.txt;g"
```

而不是在每次 LoadLibraryEx 调用进程内执行程序 (bp\[0x10\])，开发人员可以将其限制为仅当类安装程序，并共同安装程序 Dll 已加载到进程执行。 因为[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)类安装程序将调用的例程和注册的设备的共同安装程序，这些 Dll 将在该调用期间加载到进程。

因为这些 Dll 将从卸载程序时，应有关所不做的任何假设*DrvInst.exe*主机进程中，您必须确保断点可以处理对所做的任何调用的过程找到DLL入口点**SetupDiCallClassInstaller**从*DrvInst.exe*主机进程。

```cpp
kd> bd[0x10]
kd> bp[0x11] /p @$proc setupapi!SetupDiCallClassInstaller "be[0x10];bp[0x12] /p @$proc @$ra \"bd[0x10];bc[0x12];g\";g"
kd> g
```

若要执行调试器命令程序的断点 (bp\[0x10\]) 最初处于禁用状态。 已启用每当[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)调用 (bp\[0x11\])，并继续执行。 调试器命令程序 (bp\[0x10\]) 时再次禁用**SetupDiCallClassInstaller**返回由该例程本身返回地址上设置断点 (bp\[0x12\]).

请注意，禁用调试器命令程序断点也清除了自身，将继续执行，直至[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)试或安装之前，调用程序完成并清除所有断点 (bp\[0x13\])。

执行开始时设置上述断点后，该过程将中断 mycoinst 每次调用 ！CoInstallerProc。 这样，您可以调试类安装程序或辅助安装程序 DLL 核心设备安装过程的执行。

默认值才能完成安装过程的时间段为 5 分钟。 如果在给定的时间段内未完成该过程，系统将认为该过程已停止响应，并将它终止。

放置在设备安装的默认超时限制时通过内核调试程序在调试进程所做的更改。 由于中断到调试器时停止执行的系统上的所有程序，则安装过程所花费的时间量将跟踪会将未经调试的系统上的相同。

 

 





