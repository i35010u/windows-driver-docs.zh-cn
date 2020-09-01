---
title: 使用 KMDF 验证程序
description: 使用 KMDF 验证程序
ms.assetid: ab6a0149-9341-435b-b7e7-9c5d6520ebd8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10fe4d932aad730bcdcff2a6b57569e9d9e0f265
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188135"
---
# <a name="using-kmdf-verifier"></a>使用 KMDF 验证程序


该框架提供了可用于测试正在运行的 KMDF 驱动程序的内置验证功能。 此功能称为 KMDF Verifier，广泛验证驱动程序的状态和驱动程序传递给框架对象方法的参数。 您可以单独使用框架的验证程序，也可以结合使用常规用途的 [驱动程序验证程序 ( # A0) ](../devtest/driver-verifier.md) 工具。

如果启用了 KMDF Verifier，框架将检查锁获取和层次结构，确保对框架的调用以正确的 IRQL 出现，验证正确的 i/o 取消和队列使用情况，并确保驱动程序和框架遵循记录的协定。 它还可以模拟内存不足的情况，以便驱动程序开发人员可以测试驱动程序是否正确响应，而无需崩溃、挂起或卸载。

如果启用了 KMDF 验证程序，则当默认超时期限为60秒时，框架会中断到调试器，直到前面介绍的某些事件完成。 此时，您可以调试问题，或在调试器中键入 "g" 来重新启动超时期限。 使用[控制验证程序行为](#controlling-the-verifiers-behavior)中所述的**DbgWaitForSignalTimeoutInSec**注册表值，可以更改默认超时期限。

建议在测试期间运行 ( # A0) 的驱动程序验证程序，并将自己的驱动程序和 wdf01000.sys 添加到验证列表。

如果你的驱动程序是用 KMDF 1.9 版或更高版本生成的，并且你 Verifier.exe 运行，则会自动启用 KMDF Verifier。

你还可以使用 [WDF 验证器控件应用程序 ( # A0) ](../devtest/wdf-verifier-control-application.md) 来启用和禁用 KMDF 验证程序。

## <a name="enabling-and-disabling-the-frameworks-built-in-verification"></a>启用和禁用框架的内置验证


你可以使用以下过程手动启用 KMDF 验证程序：

1.  如果已加载了驱动程序，请使用设备管理器禁用该设备。 禁用该设备将导致卸载该驱动程序。
2.  在 Windows 注册表中，使用 RegEdit 将 **VerifierOn** 设置为驱动程序的 **参数 \\ Wdf** 子项中 **的 \_ 非 \_ \\ \\ \\ ** 零值。 非零值表示启用了 KMDF Verifier。

    如果子项不存在，你可能需要手动将 **VerifierOn** 添加到该子项。

3.  使用设备管理器重新启用设备，从而加载驱动程序。
4.  当驱动程序调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)时，框架将检查注册表，如果 **VerifierOn** 为非零值，则会启用框架的验证程序。

若要禁用框架的验证程序，请执行相同的步骤，但将 **VerifierOn** 的值设置为零。

若要确定是否已启用框架的验证程序，请在驱动程序调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 后在某个位置设置断点，并使用 [**！ wdfdriverinfo**](../debugger/-wdfkd-wdfdriverinfo.md) 调试器扩展命令：

**！ wdfkd. wdfdriverinfo** * &lt; drivername &gt; *  ****  **0x1**

有关调试器扩展命令的详细信息，请参阅 [基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

## <a name="controlling-the-verifiers-behavior"></a>控制验证程序的行为


建议使用 [WDF 验证器控件应用程序](../devtest/wdf-verifier-control-application.md) 来控制以下选项。 但是，你可以直接修改注册表中的以下值。

相关值位于**HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services** key 的 Parameters 项子键下。 ** \\ **

<a href="" id="verifyon-----------------reg-dword-"></a>**VerifyOn** (**REG \_ DWORD**)   
将此值设置为一个非零值，以启用 [**WDFVERIFY**](./wdfverify.md) 宏。

<a href="" id="dbgbreakonerror-----------------------------reg-dword-"></a>**DbgBreakOnError** (**REG \_ DWORD**)   
如果此值设置为非零值，则在每次驱动程序调用 [**WdfVerifierDbgBreakPoint**](/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)时，框架都将中断到调试器)  (。

<a href="" id="dbgwaitforsignaltimeoutinsec---------------reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG \_ DWORD**)   
从 Windows 8 开始，当 **VerifierOn** 和 **DbgBreakOnError** 设置为非零值时，驱动程序可以通过设置 **DbgWaitForSignalTimeoutInSec**来更改默认超时时间。

<a href="" id="verifierallocatefailcount------------------------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG \_ DWORD**)   
如果此值设置为值 *n*，则在第 *n* 个分配后，框架将无法每次尝试为驱动程序的对象分配内存。

<a href="" id="trackhandles---------------reg-multi-sz-"></a>**TrackHandles** (**REG \_ 多 \_ SZ**)   
如果此值设置为框架对象句柄的一个或多个类型名称的列表，则框架将跟踪与指定的句柄类型匹配的所有对象句柄的引用。

<a href="" id="enhancedverifieroptions-----------------------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG \_ DWORD**)   
**仅 KMDF**

包含一个可用于启用框架的验证程序的可选功能的位图。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** (**REG \_ DWORD**)   
如果设置为非零值，并且该驱动程序是使用比当前版本旧的 framework 版本生成的，则该框架的验证程序将包含在生成驱动程序之后添加的测试。

一般规则是，如果设置上述注册表值，请在不再需要这些值时将其删除。

有关这些注册表值的完整说明，请参阅 [用于调试基于框架的驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。

 

