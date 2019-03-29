---
title: 使用 KMDF 验证程序
description: 使用 KMDF 验证程序
ms.assetid: ab6a0149-9341-435b-b7e7-9c5d6520ebd8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 988f631c9ecd8c89fcba22eb6594bb252cf14e29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562160"
---
# <a name="using-kmdf-verifier"></a>使用 KMDF 验证程序


该框架提供可用于测试正在运行的 KMDF 驱动程序的内置验证功能。 此功能，称为 KMDF 验证程序，广泛验证驱动程序的状态和驱动程序将传递给框架对象方法的参数。 您可以使用框架的验证程序本身，或者与常规用途[Driver Verifier (Verifier.exe)](https://msdn.microsoft.com/library/windows/hardware/ff545448)工具。

如果启用了 KMDF 验证工具，该框架检查锁获得和层次结构，确保对该框架的调用出现在正确的 IRQL、 验证正确的 I/O 取消和队列使用情况，并确保按照已编档的驱动程序和框架协定。 它还可以模拟内存不足条件，以便驱动程序开发人员可以测试是否驱动程序崩溃、 挂起，或无法卸载无做出正确响应。

启用 KMDF 验证工具后，框架会进入调试器如果 60 秒的默认超时期限过期之前所述的事件的一些以前已完成。 此时，可以调试该问题，或重新启动的超时期限在调试器中键入"g"。 可以使用更改默认超时期限**DbgWaitForSignalTimeoutInSec**注册表值中所述[控制验证程序的行为](#verifier-reg-values)。

建议运行 Driver Verifier (Verifier.exe) 在测试和验证列表中添加你自己的驱动程序和 wdf01000.sys 过程。

如果您的驱动程序已使用 KMDF 1.9 或更高版本生成和运行 Verifier.exe，会自动启用 KMDF 验证程序。

此外可以使用[WDF 验证程序控件应用程序 (WdfVerifier.exe)](https://msdn.microsoft.com/library/windows/hardware/ff556129)来启用和禁用 KMDF 验证程序。

## <a name="enabling-and-disabling-the-frameworks-built-in-verification"></a>启用和禁用框架的内置验证


您可以手动启用 KMDF 验证程序使用此过程：

1.  如果尚未加载您的驱动程序，使用设备管理器禁用设备。 禁用设备会导致无法卸载该驱动程序。
2.  使用注册表编辑器设置**VerifierOn**为非零值中的驱动程序**参数\\Wdf**的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\服务**Windows 注册表中的键。 一个非零值指示启用了 KMDF 验证程序。

    可能需要添加**VerifierOn**手动为如果尚未存在的子项。

3.  使用设备管理器重新启用该设备，从而加载驱动程序。
4.  当驱动程序调用[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)，框架会检查注册表，并启用框架的验证程序，如**VerifierOn**为非零值。

若要禁用框架的验证程序，请按照相同的步骤，但设置的值**VerifierOn**为零。

若要确定是否启用框架的验证程序，设置断点的位置后驱动程序调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175) ，并使用[ **！ wdfdriverinfo**](https://msdn.microsoft.com/library/windows/hardware/ff565724)调试器扩展命令：

**!wdfkd.wdfdriverinfo** *&lt;your drivername&gt;* **** **0x1**

有关调试器扩展命令的详细信息，请参阅[基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

## <a name="controlling-the-verifiers-behavior"></a>控制验证程序的行为


我们建议你使用[WDF 验证程序控件应用程序](https://msdn.microsoft.com/library/windows/hardware/ff556129)来控制以下选项。 但是，可以直接修改注册表中的以下值。

相关值位于**参数\\Wdf**的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\服务**密钥。

<a href="" id="verifyon-----------------reg-dword-"></a>**VerifyOn** (**REG\_DWORD**)  
将此值设置为非零值，以启用[ **WDFVERIFY** ](https://msdn.microsoft.com/library/windows/hardware/ff551167)宏。

<a href="" id="dbgbreakonerror-----------------------------reg-dword-"></a>**DbgBreakOnError** (**REG\_DWORD**)  
如果此值设置为非零值，该框架将在调试器中中断 （如果可用） 每次将驱动程序要求[ **WdfVerifierDbgBreakPoint**](https://msdn.microsoft.com/library/windows/hardware/ff551164)。

<a href="" id="dbgwaitforsignaltimeoutinsec---------------reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG\_DWORD**)  
在 Windows 8 中，启动时**VerifierOn**并**DbgBreakOnError**设置为非零值，该驱动程序可以通过设置更改默认超时期限**DbgWaitForSignalTimeoutInSec**.

<a href="" id="verifierallocatefailcount------------------------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG\_DWORD**)  
如果此值设置为值*n*，framework 将失败，每次尝试为驱动程序的对象分配内存*第 n 个*分配。

<a href="" id="trackhandles---------------reg-multi-sz-"></a>**TrackHandles** (**REG\_多\_SZ**)  
如果此值设置为一个或多个框架对象句柄的类型名称的列表，该框架会跟踪对与指定句柄类型匹配的所有对象句柄的引用。

<a href="" id="enhancedverifieroptions-----------------------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG\_DWORD**)  
**仅 KMDF**

包含可用于启用框架的验证程序的可选功能的位图。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** (**REG\_DWORD**)  
如果设置为非零值，和框架的验证程序如果驱动程序使用早于当前版本的 framework 版本生成，包括驱动程序已生成后已添加的测试。

作为一般规则，如果将设置以上注册表值，删除它们在不再需要时。

这些注册表值的完整说明，请参阅[调试 Framework 基于驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。

 

 





