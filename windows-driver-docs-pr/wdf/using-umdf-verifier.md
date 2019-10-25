---
title: 使用 UMDF 验证程序
description: 使用 UMDF 验证程序
ms.assetid: 95D85894-86AF-4312-B5BD-F1C9E8F8B2E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06870c6c89dd3624c0e3e912eb7a06f53c394534
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842589"
---
# <a name="using-umdf-verifier"></a>使用 UMDF 验证程序


此框架提供内置验证功能，可用于测试正在运行的用户模式驱动程序框架（UMDF）驱动程序。 此功能有时称为 UMDF 验证程序，广泛验证驱动程序的状态和驱动程序传递给框架对象方法的参数。 可以单独使用 UMDF 验证程序，也可以结合使用常规用途的[应用程序验证工具（AppVerif）](../debugger/debugger-download-tools.md)工具。

UMDF 验证程序检查锁获取和层次结构，验证正确的 i/o 取消和队列使用情况，并确保驱动程序和框架遵循记录的协定。

UMDF 验证程序导致 UMDF 驱动程序代码中的*错误检查*主机进程。 但是，UMDF bug 检查不会显示蓝色文本屏幕，并显示有关错误的信息。 相反，UMDF bug 检查：

-   创建内存转储文件，并将文件保存到计算机的日志文件目录（例如% windir%\\System32\\日志文件\\WUDF\\*Xxx*）。

    **请注意**  在 UMDF 2.15 开始，日志目录为 *% ProgramData%* \\Microsoft\\WDF。

     

-   为 Microsoft 创建[错误报告](how-umdf-reports-errors.md)（选择加入）。

-   如果已连接到计算机，则中断调试器。

-   终止宿主进程并禁用该设备。

从 UMDF 2.0 开始，UMDF 验证程序在某些情况下会发出断点，并导致其他情况下的 UMDF bug 检查。 此行为类似于 KMDF 验证程序的行为。

在 WUDFHost 上启用[应用程序验证工具（AppVerif）](../debugger/debugger-download-tools.md)后，我们强烈建议对驱动程序进行所有的开发和测试。 使用以下命令，附加调试器，然后重新启动。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

从 UMDF 版本2.0 开始，如果在驱动程序主机进程（Wudfhost）上运行[应用程序验证工具](../debugger/debugger-download-tools.md)，则会自动为该主机中的所有 umdf 2.0 驱动程序启用 umdf 验证程序，并在将来的驱动程序主机进程中为所有 umdf 2.0 驱动程序启用该程序。

在 UMDF 1.11 及更早版本中，框架的验证器始终处于打开状态，你无法将其关闭。

## <a name="enabling-and-disabling-umdf-verifier"></a>启用和禁用 UMDF 验证程序


可以通过将**VerifierOn**的 **\\参数**设置为非零值，来手动启用 UMDF 验证程序，方法是将**HKEY\_本地\_机\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;驱动程序名称&gt;** 注册表项。

**请注意**，  **VerifierOn**值是否存在，甚至设置为零，都将覆盖应用程序验证工具的链接。 因此，如果不强制执行此值，建议删除该值，而不是将其设置为零。

 

若要确定是否启用了 UMDF 验证程序，请在驱动程序调用[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)后在某个位置设置断点，并使用[ **！ wdfdriverinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)调试器扩展命令：

**！ wdfkd. wdfdriverinfo** *&lt;你的 drivername&gt;*  **** **0x1**

有关调试器扩展命令的详细信息，请参阅[基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

## <a name="controlling-the-verifiers-behavior"></a>控制验证程序的行为


可以通过修改注册表中的值来控制 UMDF 验证程序的行为。 或者，您可以使用[WDF 验证程序控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)来设置这些值。

以下注册表值可以与 UMDF 1 一起使用。*x*驱动程序以及 UMDF 2.0 和更高版本的驱动程序。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** （**REG\_DWORD**）  
如果将**VerifyDownLevel**设置为非零值，并且该驱动程序是使用比当前版本旧的 framework 版本生成的，则该框架的验证程序将包含在生成驱动程序之后添加的测试。 如果此值不存在或设置为零，则框架的验证器将仅包含生成驱动程序时存在的测试。

例如，如果你的驱动程序是用 framework 1.7 版构建的，并且如果计算机上安装了 framework 版本1.9，则将**VerifyDownLevel**设置为非零会导致验证程序包含已添加到 verifier 版本1.9 的测试当驱动程序运行时。

此值位于 HKEY 的**参数\\Wdf**子项 **\_本地\_机\\软件\\MICROSOFT\\Windows NT\\CurrentVersion\\WUDF\\Services\\*DriverName*** 注册表项。

<a href="" id="trackobjects-----------------------------reg-dword-"></a>**TrackObjects** （**REG\_DWORD**）  
如果将**TrackObjects**设置为非零值，则当卸载驱动程序时，框架将进入调试器，如果任何基于框架的对象[泄漏](determining-if-a-driver-leaks-framework-objects.md)（未删除）。

在常规测试过程中，应启用**TrackObjects**而不是**TrackRefCounts**。 如果验证程序报告驱动程序正在泄漏框架对象，请使用 control 应用程序启用**TrackRefCounts** verifier 选项。

此值位于**HKEY\_本地\_计算机\\软件\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\Services**注册表项的*DefaultHostProcessGuid*子项，其中*DefaultHostProcessGuid*是可在**HKEY\_本地\_计算机\\软件\\MICROSOFT\\Windows NT\\CurrentVersion\\WUDF**子项中查找的值。

<a href="" id="trackrefcounts-----------------------------reg-dword-"></a>**TrackRefCounts** （**REG\_DWORD**）  
如果**TrackRefCounts**设置为非零值，则框架将维护对每个基于框架的对象的引用数的计数。 您可以使用[！ wudfrefhist](using-umdf-debugger-extensions.md)调试器扩展来查看对象的引用计数的更改。

将**TrackRefCounts**设置为非零值将降低驱动程序的性能，因此应将值保留为零，除非正在调试对象删除 bug。

此值位于**HKEY\_本地\_计算机\\软件\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\Services**注册表项的*DefaultHostProcessGuid*子项，其中*DefaultHostProcessGuid*是可在**HKEY\_本地\_计算机\\软件\\MICROSOFT\\Windows NT\\CurrentVersion\\WUDF**子项中查找的值。

除了上面列出的注册表值，UMDF 2.0 和更高版本的驱动程序还可以使用[使用 KMDF Verifier](using-kmdf-verifier.md)中列出的许多注册表值。

 

 





