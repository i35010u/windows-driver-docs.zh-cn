---
title: 使用内核调试程序 (KD) 调试设备安装
description: 使用内核调试程序 (KD) 调试设备安装
ms.assetid: 0967d375-2602-44d2-b4ac-8d1e112afc3f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d45ef0a76df81e698628b9b19db1ff40c671f51
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715598"
---
# <a name="debugging-device-installations-with-the-kernel-debugger-kd"></a>使用内核调试程序 (KD) 调试设备安装


从 Windows Vista 开始，当即插即用 (PnP) manager 在系统中检测到新设备时，操作系统将启动设备安装主机进程 (*DrvInst.exe*) 搜索并安装设备驱动程序。

由于设备安装在此用户模式进程内进行，因此，通常使用用户模式调试程序时，可以使用用户模式 [调试器，如调试设备安装](debugging-device-installations-with-a-user-mode-debugger.md)中所述。 但是，在某些情况下，使用内核调试器 (KD) 来监视用户模式设备安装过程可能会有所帮助。

例如，在调试用户模式设备安装时，通过使用 KD，你可以执行以下操作：

-   使用！ devnode、！ devobj、！ drvobj、！ irp 和其他 KD 扩展同时调试内核模式问题。

-   监视其他用户模式进程，而无需使用 KD extension！ process 或. process/p。管理多个调试器

有关 KD 和其他调试工具的详细信息，请参阅 [Windows 调试](../debugger/index.md)。

**DebugInstall**注册表值指定在系统上启用的设备安装调试支持的类型。 有关此注册表值的详细信息，请参阅 [启用对调试设备安装的支持](enabling-support-for-debugging-device-installations.md)。

将 **DebugInstall** 注册表值设置为1时， *DrvInst.exe* 将首先检查内核调试器是否已启用，当前是否已附加到调试器中。 在进行此中断后，可以在当前进程的用户模式模块中设置断点。 例如：

```cpp
kd> .reload /user
kd> bp /p @$proc setupapi!SetupDiCallClassInstaller
```

这会在例程 SETUPAPI.LOG 上设置一个断点！仅适用于当前进程的 SetupDiCallClassInstaller。

对于 [驱动程序包](driver-packages.md)的开发人员而言，在安装设备的过程中，通常最需要调试类安装程序或共同安装程序 DLL 的操作。 但是，当 *DrvInst.exe* 中断调试器时，驱动程序包中的任何类安装程序或共同安装程序 dll 都将不会加载。 尽管用户模式调试器支持在使用 "sx e ld" 命令将用户模式模块加载到进程中时设置调试器异常的功能，但内核调试器只支持使用该命令的内核模式模块。

下面的代码示例演示了 "调试器命令程序" 如何监视特定类安装程序或共同安装程序到当前进程的加载。 在此示例中，调试程序命令程序将在主入口点上设置一个断点 (*Mycoinst.dll* 联安装程序的 CoInstallerProc) ：

```cpp
file: Z:\bpcoinst.txt

r $t1 = 0
!for_each_module .if ($spat("@#ModuleName", "mycoinst*") = 0) {r $t1 = 1}
.if (not @$t1 = 0) {.echo mycoinst is loaded, set bp on mycoinst!CoInstallerProc } .else {.echo mycoinst not loaded}
.if (not @$t1 = 0) {.reload mycoinst.dll}
.if (not @$t1 = 0) {bp[0x20] /p @$proc mycoinst!CoInstallerProc } .else {bc[0x20]}
```

执行时，调试器命令程序将检查加载到 *Mycoinst.dll*的当前进程中的模块列表。 加载此共同安装程序 DLL 后，调试器将使用 CoInstallerProc 入口点函数上的已知断点 ID) 设置断点 (。

从 *DrvInst.exe* 主机进程启动的调试断点开始，你应该首先在调用的返回地址上设置一个断点，其中 *DrvInst.exe* 分解为内核调试器。 此断点将清除在设备安装过程中设置的所有断点，并继续执行：

```cpp
DRVINST.EXE: Entering debugger during PnP device installation.
Device instance = "X\Y\Z" ...

Break instruction exception - code 80000003 (first chance)
010117b7 cc               int     3

kd> bp[0x13] /p @$proc @$ra "bc *;g"
```

接下来，应在进程内设置一些断点，以允许调试器命令程序中的命令在设备安装过程中的适当时间执行。

若要确保在为设备安装调用函数之前设置类安装程序或共同安装程序 DLL 入口点的断点，应在将新的 DLL 加载到当前进程中时执行调试器命令程序，也就是说，在对 LoadLibraryExW 的调用返回之后：

```cpp
kd> .reload
kd> bp[0x10] /p @$proc kernel32!LoadLibraryExW "gu;$$><Z:\\bpcoinst.txt;g"
```

\[ \] 开发人员可以将其限制为仅在将类安装程序和共同安装程序 dll 加载到进程中的每个 LoadLibraryEx 调用上执行程序，而不是在)  (过程中执行此程序。 由于 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 是调用为某个设备注册的类安装程序和共同安装程序的例程，因此这些 dll 将在该调用期间加载到进程中。

因为在从*DrvInst.exe*主机进程中卸载这些 dll 时，不应进行任何假设，所以必须确保在从*DrvInst.exe*主机进程对**SetupDiCallClassInstaller**进行的任何调用期间，断点都可以处理定位 DLL 入口点。

```cpp
kd> bd[0x10]
kd> bp[0x11] /p @$proc setupapi!SetupDiCallClassInstaller "be[0x10];bp[0x12] /p @$proc @$ra \"bd[0x10];bc[0x12];g\";g"
kd> g
```

最初禁用 (bp 0x10) 执行调试器命令程序的断点 \[ \] 。 无论何时调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 都 (bp 0x11) ，都将启用此功能 \[ \] ，并且继续执行。 当 SetupDiCallClassInstaller 返回时，将再次禁用调试程序命令 (程序 \[ \]) ，方法是在该例程本身 (bp 0x12) 的返回地址上设置断点**SetupDiCallClassInstaller** \[ \] 。

请注意，禁用调试器命令程序的断点还会自行清除，并继续执行，直到再次调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 或直到安装程序完成，并 (bp 0x13) 中清除所有断点 \[ \] 。

如果在设置上述断点后开始执行，则进程将在每次调用 mycoinst 时中断！CoInstallerProc. 这允许您在核心设备安装过程中调试类安装程序或共同安装程序 DLL 的执行。

完成安装过程的默认时间段为5分钟。 如果该进程未在给定的时间段内完成，系统会假定该进程已停止响应，并被终止。

在通过内核调试器进行调试的过程中，设备安装上的默认超时限制仍有效。 由于在中断到调试器时系统上的所有程序的执行都将停止，因此将跟踪安装进程所用的时间，这与在未调试的系统上的跟踪相同。

 

