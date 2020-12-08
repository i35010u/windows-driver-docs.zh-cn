---
title: 确定驱动程序是否泄漏框架对象
description: 本主题介绍了如何查找由未发布引用引起的驱动程序内存泄漏。 它适用于 User-Mode Driver Framework (UMDF) 第1版和第2版驱动程序。
keywords:
- 调试方案 WDK UMDF，确定驱动程序是否泄漏框架对象
- UMDF WDK，调试方案，确定驱动程序是否泄漏框架对象
- UMDF WDK，确定驱动程序是否泄漏框架对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a99c761428087fc45e7e64caf03cb2830ce712c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828975"
---
# <a name="determining-if-a-driver-leaks-framework-objects"></a>确定驱动程序是否泄漏框架对象


本主题介绍了如何查找由未发布引用引起的驱动程序内存泄漏。 它适用于 User-Mode Driver Framework (UMDF) 第1版和第2版驱动程序。

## <a name="umdf-1"></a>UMDF 1


在 UMDF 版本1中，如果对 **AddRef** 的每次调用没有匹配的 **Release** 调用，则调用堆栈可能会导致内存泄漏。

若要测试 UMDF 版本1驱动程序是否泄漏框架对象，请使用以下步骤：

1.  使用 [WDF 验证器控件应用程序](../devtest/wdf-verifier-control-application.md) 设置所需的验证程序选项。 在常规测试过程中，首先设置 **TrackObjects** ，而不是 **TrackRefCounts**。

    卸载驱动程序时，如果未删除框架对象，框架的代码验证器将进入调试器，并提示你使用 [**！ wudfdumpobjects**](using-umdf-debugger-extensions.md) 调试器扩展。 此调试器扩展显示删除的对象的列表。

2.  如果代码验证器表明驱动程序正在泄漏框架对象，请使用 control 应用程序设置 [**TrackRefCounts**](using-umdf-verifier.md) 选项。

    如果设置了此选项，则在驱动程序运行时，验证程序将跟踪对框架对象的引用。 您可以使用 [**！ wudfrefhist**](using-umdf-debugger-extensions.md) 调试器扩展显示每个调用堆栈 (一组函数调用，这些调用堆栈递增或递减对象的引用计数) 。 通过检查这些调用堆栈中的 **AddRef** 和 **Release** 调用，你应该能够找到一个堆栈，该堆栈不会减少对象的引用计数，进而导致泄漏。

有关其他验证程序选项的信息，请参阅 [使用 UMDF 验证](using-umdf-verifier.md)程序。

有关何时删除框架对象的信息，请参阅 [管理对象的生存期](managing-the-lifetime-of-objects.md)。

## <a name="umdf-2"></a>UMDF 2


在 UMDF 版本2中，未发布引用非常罕见，但由于使用 [**WdfObjectReference**](./wdfobjectreference.md) 和 [**WdfObjectDereference**](./wdfobjectdereference.md)时调用不匹配，可能会出现这种情况。

若要测试 UMDF 版本2驱动程序是否泄漏框架对象，请使用以下过程：

1.  按照 [最佳做法](enabling-a-debugger.md#bp) 中所述的步骤配置计算机以进行 UMDF 调试。
2.  若要使用标记跟踪，请在注册表中同时启用 UMDF 验证程序和句柄跟踪。 这两个设置都存储在 **HKEY \_ 本地 \_ 计算机 \\ SOFTWARE \\ Microsoft \\ Windows NT \\ CurrentVersion \\ WUDF \\ Services \\ &lt; 驱动程序名称 &gt;** 密钥的驱动程序的 **参数 \\ Wdf** 子项中。

    若要启用 UMDF 验证程序，请为 VerifierOn 设置非零值 **。**

    若要启用句柄跟踪，请将 **TrackHandles** 的值设置为一个或多个对象类型的名称，或指定星号 (\*) 以跟踪所有对象类型。

    你还可以使用 [WdfVerifier.exe](../devtest/wdf-verifier-control-application.md) 应用程序修改 UMDF 验证程序设置。

3.  重新启动，建立调试器连接，然后使用以下调试器命令：

    -   [**！ wdfkd wdfdriverinfo 0x10**](../debugger/-wdfkd-wdfdriverinfo.md) 以显示句柄层次结构
    -   [**！ wdfkd wdftagtracker**](../debugger/-wdfkd-wdftagtracker.md) 显示标记信息

如果启用了 UMDF 验证程序，则会在卸载驱动程序时检测内存泄漏，就像在 KMDF 中一样。

有关在 KMDF 和 UMDF 版本2驱动程序中使用引用计数的其他信息，请参阅 [框架对象生命周期](framework-object-life-cycle.md)。

 

