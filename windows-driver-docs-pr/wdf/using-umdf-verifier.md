---
title: 使用 UMDF 验证程序
description: 使用 UMDF 验证程序
ms.assetid: 95D85894-86AF-4312-B5BD-F1C9E8F8B2E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7119e957b86704e1c3eb04aa9490cd4f9816915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372172"
---
# <a name="using-umdf-verifier"></a>使用 UMDF 验证程序


该框架提供可用于测试正在运行的用户模式驱动程序框架 (UMDF) 驱动程序的内置验证功能。 此功能，有时称为 UMDF 验证程序，广泛验证驱动程序的状态和驱动程序将传递给框架对象方法的参数。 可以使用 UMDF 验证工具本身，或者与常规用途[应用程序验证器 (AppVerif.exe)](../debugger/debugger-download-tools.md)工具。

UMDF 验证工具检查锁获得和层次结构、 验证正确的 I/O 取消和队列使用情况，并确保驱动程序和框架，单击有案可稽的协定。

UMDF Verifier 到 UMDF 驱动程序代码中将导致失败*bug 检查*主机进程。 但是，UMDF bug 检查不会导致一个蓝色文本屏幕来显示有关错误的信息。 相反，UMDF bug 检查：

-   创建内存转储文件，并将该文件保存到计算机的日志文件目录 (例如，%windir%\\System32\\LogFiles\\WUDF\\*Xxx*.dmp)。

    **请注意**  UMDF 2.15 从开始，日志目录是 *%programdata%* \\Microsoft\\WDF。

     

-   创建[错误报告](how-umdf-reports-errors.md)microsoft （选择在）。

-   如果一个连接到计算机，进入调试器。

-   终止主机进程，并禁用的设备。

从 UMDF 2.0 开始，UMDF Verifier 问题在某些情况下，断点，并在其他导致 UMDF bug 检查。 此行为是类似于 KMDF 验证程序。

我们强烈建议进行所有开发和测试您的驱动程序的启用后[应用程序验证器 (AppVerif.exe)](../debugger/debugger-download-tools.md) WUDFHost.exe 上。 使用以下命令，附加调试器，然后重新启动。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

从版本 2.0 的 UMDF，如果在运行[应用程序验证工具](../debugger/debugger-download-tools.md)驱动程序主机进程 (Wudfhost)，在 UMDF 验证工具会自动启用来在该主机中的所有 UMDF 2.0 驱动程序，以及在未来的驱动程序主机中的所有 UMDF 2.0 驱动程序处理。

在 UMDF 1.11 和更早版本，框架的验证程序始终在并且不能将其关闭。

## <a name="enabling-and-disabling-umdf-verifier"></a>启用和禁用 UMDF 验证工具


您可以通过设置手动启用 UMDF Verifier **VerifierOn**为非零值中的驱动程序**参数\\Wdf**的子项**HKEY\_本地\_机器\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;驱动程序名称&gt;** 注册表项。

**请注意**  是否存在**VerifierOn**根本，即使设置为零，值将覆盖与应用程序验证工具的链接。 因此，我们建议删除值，如果您在不强制它，而不将其设置为零。

 

若要确定是否启用 UMDF 验证工具，设置断点的位置后驱动程序调用[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate) ，并使用[ **！ wdfdriverinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)调试器扩展命令：

**!wdfkd.wdfdriverinfo** *&lt;your drivername&gt;*  **** **0x1**

有关调试器扩展命令的详细信息，请参阅[基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

## <a name="controlling-the-verifiers-behavior"></a>控制验证程序的行为


可以通过修改注册表中的值来控制 UMDF 验证程序的行为。 或者，可以使用[WDF 验证程序控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)来设置这些值。

以下注册表值，可以在 UMDF 1。*x*驱动程序，以及 UMDF 2.0 及更高版本的驱动程序。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** (**REG\_DWORD**)  
如果**VerifyDownLevel**设置为非零值，和框架的验证程序如果驱动程序使用早于当前版本的 framework 版本生成，包括驱动程序已生成后已添加的测试。 如果此值不存在，或者设置为零，框架的验证程序包括仅存在于该驱动程序生成时的测试。

例如，如果您的驱动程序生成为版本 1.7 的框架，并且计算机上安装的 framework 版本 1.9，设置**VerifyDownLevel**不为零将导致的验证程序，包括已添加到的测试当您的驱动程序运行时的验证程序 1.9 版中。

此值位于**参数\\Wdf**的子项**HKEY\_本地\_机\\软件\\Microsoft\\WindowsNT\\CurrentVersion\\WUDF\\Services\\* DriverName*** 注册表项。

<a href="" id="trackobjects-----------------------------reg-dword-"></a>**TrackObjects** (**REG\_DWORD**)  
如果**TrackObjects**设置为非零值，该框架时，将进入调试器的驱动程序已被卸载，如果基于 framework 的所有对象都具有[泄漏](determining-if-a-driver-leaks-framework-objects.md)(未删除)。

正则在测试期间，应启用**TrackObjects**而不**TrackRefCounts**。 如果验证程序报告该驱动程序正在泄漏 framework 对象，然后使用控制应用程序以启用**TrackRefCounts** verifier 选项。

此值位于*DefaultHostProcessGuid*的子项**HKEY\_本地\_机\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services**注册表项，其中*DefaultHostProcessGuid*是一个值，您可以在中找到该值**HKEY\_本地\_机器\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**子项。

<a href="" id="trackrefcounts-----------------------------reg-dword-"></a>**TrackRefCounts** (**REG\_DWORD**)  
如果**TrackRefCounts**设置为非零值，该框架维护对每个基于框架的对象的引用数的计数。 可以使用[！ wudfrefhist](using-umdf-debugger-extensions.md)调试器扩展，以查看对象的引用计数的更改。

设置**TrackRefCounts**为非零值会降低，驱动程序的性能，因此，应该在零处保留值，除非你正在调试对象删除 bug。

此值位于*DefaultHostProcessGuid*的子项**HKEY\_本地\_机\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services**注册表项，其中*DefaultHostProcessGuid*是一个值，您可以在中找到该值**HKEY\_本地\_机器\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**子项。

除了注册表上面列出的值、 UMDF 2.0 和更高版本的驱动程序还可以使用许多中列出的注册表值[使用 KMDF Verifier](using-kmdf-verifier.md)。

 

 





