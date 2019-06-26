---
title: 确定驱动程序是否泄漏框架对象
description: 本主题介绍如何查找未释放引用导致的驱动程序内存泄漏。 它适用于用户模式驱动程序框架 (UMDF) 版本 1 和 2 的驱动程序。
ms.assetid: 617cc678-e0db-4d2f-9d19-34b6cedad234
keywords:
- WDK UMDF，确定驱动程序是否泄漏 framework 对象的调试方案
- UMDF WDK，调试方案，用于确定驱动程序是否泄漏 framework 对象
- UMDF WDK，确定驱动程序是否泄漏 framework 对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a53ff81154cabcd787cd939eb5d135f8e4ce26c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377445"
---
# <a name="determining-if-a-driver-leaks-framework-objects"></a>确定驱动程序是否泄漏框架对象


本主题介绍如何查找未释放引用导致的驱动程序内存泄漏。 它适用于用户模式驱动程序框架 (UMDF) 版本 1 和 2 的驱动程序。

## <a name="umdf-1"></a>UMDF 1


在 UMDF 版本 1，调用堆栈可能会导致内存泄漏如果每个调用**AddRef**不具有匹配**发行**调用。

若要测试是否 UMDF 驱动程序版本 1 泄漏 framework 对象，使用以下步骤：

1.  使用[WDF 验证程序控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)设置所需的验证程序选项。 正则在测试期间，开始通过设置**TrackObjects**而不**TrackRefCounts**。

    如果未删除 framework 对象，并且它会提示你使用框架的代码验证程序卸载该驱动程序时，进入调试器[ **！ wudfdumpobjects** ](using-umdf-debugger-extensions.md)调试器扩展。 此调试器扩展显示的撤消删除的对象的列表。

2.  如果代码验证程序指示驱动程序正在泄漏 framework 对象，然后使用控制应用程序设置[ **TrackRefCounts** ](using-umdf-verifier.md)选项。

    如果设置此选项，验证人将跟踪的驱动程序运行时的 framework 对象的引用。 可以使用[ **！ wudfrefhist** ](using-umdf-debugger-extensions.md)调试器扩展，以显示每个调用堆栈 （函数调用的集） 递增或递减对象的引用计数。 通过检查**AddRef**并**发行**调用在这些调用堆栈，因此应该能够找到不减小对象的引用计数，从而导致泄漏的堆栈。

有关其他验证程序选项的信息，请参阅[使用 UMDF Verifier](using-umdf-verifier.md)。

有关何时删除 framework 对象的信息，请参阅[管理对象生存期](managing-the-lifetime-of-objects.md)。

## <a name="umdf-2"></a>UMDF 2


未释放的引用 UMDF 版本 2，在很少见，但使用时可以因调用不匹配而可能发生[ **WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)并[ **WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference).

若要测试是否 UMDF 版本 2 驱动程序泄漏 framework 对象，使用以下过程：

1.  请按照中所述的步骤[最佳做法](enabling-a-debugger.md#bp)UMDF 调试将计算机配置。
2.  若要使用跟踪标记，启用 UMDF Verifier 和跟踪在注册表中的句柄。 这两个设置都存储在驱动程序的**参数\\Wdf**的子项**HKEY\_本地\_机\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;驱动程序名称&gt;** 密钥。

    若要启用 UMDF 验证工具，请将设置为非零值**VerifierOn。**

    若要跟踪的句柄，设置的值**TrackHandles**到一个或多个对象类型的名称或指定一个星号 (\*) 用于跟踪所有对象类型。

    您还可以通过使用修改 UMDF 验证器设置[WdfVerifier.exe](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)应用程序。

3.  重新启动，建立连接调试器，并使用以下调试器命令：

    -   [ **！ wdfkd.wdfdriverinfo 0x10** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)显示句柄层次结构
    -   [ **！ wdfkd.wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)以显示标记信息

如果 UMDF 验证程序上，内存泄漏检测到在驱动程序卸载，就像 KMDF 中一样。

有关使用引用的其他信息中 KMDF 和 UMDF 版本 2 的驱动程序计数，请参阅[Framework 对象生命周期](framework-object-life-cycle.md)。

 

 





