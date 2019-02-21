---
title: 用户模式驱动程序框架方面的常见问题
description: Windows 驱动程序框架 (WDF) 是一组可用于编写在 Windows 操作系统运行的设备驱动程序的库。
ms.assetid: 0c07e514-73f9-4d24-86ad-8ac036fdbcf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85b94151a985dfdfa262cfadeaff93b2da70f24e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545359"
---
# <a name="user-mode-driver-framework-frequently-asked-questions"></a>用户模式驱动程序框架方面的常见问题


Windows 驱动程序框架 (WDF) 是一组可用于编写在 Windows 操作系统运行的设备驱动程序的库。 WDF 定义单独的驱动程序模型支持的两个框架：内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF)。 本主题提供有关 UMDF 常见问题的解答。

## <a name="which-operating-systems-can-run-umdf-drivers"></a>哪些操作系统可以运行 UMDF 驱动程序？


您可以在以下操作系统上运行 UMDF 驱动程序：

-   Windows 10
-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista
-   Windows XP

## <a name="what-is-the-most-recent-version-of-umdf"></a>什么是 UMDF 的最新版本？


在 Windows 10 和更高版本的 UMDF 版本 2 （2.0 和 2.1）。

## <a name="what-is-the-difference-between-umdf-version-2-and-the-previous-version-111-one-dot-eleven"></a>UMDF 版本 2 和以前的版本 1.11 （一个句点十一） 之间的区别是什么？


编写 UMDF 版本 2 中的驱动程序是采用 C 编程语言编写的。 此相同的驱动程序然后，可轻松地编译为 KMDF。 此外，必须根据 COM 编程模型编写 UMDF 版本 1 驱动程序。 

有关详细信息，请参阅[入门 UMDF](getting-started-with-umdf-version-2.md)。

## <a name="which-operating-systems-support-umdf-2"></a>UMDF 2 支持哪些操作系统？


UMDF 版本 2 的驱动程序运行 Windows 8.1 及更高版本。

## <a name="which-umdf-versions-can-i-build-against-in-windows-driver-kit-wdk10"></a>哪些 UMDF 版本可以生成针对在 Windows Driver Kit (WDK) 10？


您可以构建 UMDF 2.1、 2.0、 1.11，和 1.9 驱动程序使用 Windows Driver Kit (WDK) 10 和 Microsoft Visual Studio。 有关哪些版本的 Windows 可以运行使用这些 UMDF 版本生成的驱动程序的信息，请参阅[UMDF 版本历史记录](umdf-version-history.md)。

## <a name="can-i-write-part-of-my-driver-to-run-in-user-mode-and-part-in-kernel-mode"></a>可以将我的驱动程序在用户模式下运行的一部分而一部分编写在内核模式下？


是。 即使您的驱动程序需要访问某些内核模式资源或功能，您可能能够将您的驱动程序拆分成两个部分。 此方法使你可以受益于某些开发和运行在用户模式下的驱动程序的优势。

UMDF 驱动程序可以从内核模式驱动程序接收的 I/O 请求。 有关详细信息*内核模式下客户端*，请参阅[UMDF 2 驱动程序中支持内核模式下客户端](supporting-kernel-mode-clients-in-umdf-drivers.md)。

由于增加 KMDF 和 UMDF 之间的奇偶校验，但是，您将很少需要拆分驱动程序。

##  <a name="which-framework-should-i-start-with"></a>应开始使用哪个框架？


如果您的驱动程序需要的任何不太常见的功能中列出[比较 UMDF 2 功能提供给 KMDF](comparing-umdf-2-0-functionality-to-kmdf.md)，必须使用 KMDF。 对于所有其他驱动程序，您的最佳选择应为 UMDF。

如果开始使用 UMDF，决定过渡到 KMDF 的更高版本，就可以做到最小的工作量，如中所述[如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序 （和进行相反转换）](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。

## <a name="how-do-user-mode-drivers-handle-security"></a>用户模式驱动程序如何处理安全性？


UMDF 驱动程序在驱动程序主机进程，这在 LocalService 帐户的安全凭据中运行，尽管的宿主进程本身并不是 Windows 服务中运行。 因此，用户模式驱动程序是用户模式下的任何其他服务一样安全。 在 UMDF 驱动程序问题的 I/O 请求，它可以根据需要 impersonate 其客户端进程。 模拟使驱动程序线程运行客户端的安全上下文中，以便在系统执行对客户端的标识而非驱动程序主机进程的访问权限检查。

用户模式驱动程序可以模拟其客户端进程仅对于 I/O 请求，而不是插或其他系统消息。

在驱动程序安装的 INF 文件驱动程序设置最大模拟级别。 模拟应设置最低级别无法防止"特权提升"攻击。 当客户端应用程序调用**CreateFile**函数，它指定模拟级别。 然后，该驱动程序请求的每个 I/O 请求的模拟级别。

## <a name="will-a-user-mode-driver-be-fast-enough"></a>将用户模式驱动程序是速度足够快？


性能是开发 UMDF 高优先级。 虽然滞后时间和 CPU 使用率增加某种程度上，总线容量是 UMDF 支持的设备类型的主控制因素。

## <a name="what-is-the-difference-between-a-user-mode-driver-and-an-application"></a>用户模式驱动程序和应用程序之间的区别是什么？


用户模式驱动程序将启动由驱动程序管理器，并在驱动程序主机进程中运行。 驱动程序的单个实例可以同时从多个应用程序请求提供服务。 若要与该驱动程序进行通信，应用程序向驱动程序的设备通过 Win32 API 发出 I/O 请求。 用户模式驱动程序中的主入口点是[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)接口 (UMDF 1.11 及更早版本) 或[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)例程 （从 UMDF 2.0），而非**main （)** 函数。

驱动程序还包括其他接口或调用的回调，以响应 I/O 请求和插和电源通知。 UMDF 驱动程序管理的设备集成到系统并参与插和电源管理。

## <a name="how-do-i-debug-a-umdf-driver"></a>如何调试 UMDF 驱动程序？


可以通过使用用户模式下调试程序或内核模式调试程序调试 UMDF 驱动程序。 有关详细信息，请参阅[调试 WDF 驱动程序](debugging-a-wdf-driver.md)。

从 UMDF 2.0 版开始，您可以使用许多中的命令*Wdfkd.dll*调试器扩展库来调试 UMDF 驱动程序。 有关命令的列表，请参阅[调试器扩展](debugger-extensions-for-kmdf-drivers.md)。 另外，UMDF 存储 UMDF 跟踪日志 (或 UMDF *IFR*) 内核非分页内存中。 IFR 有关的信息，请参阅[使用框架的事件记录器](using-the-framework-s-event-logger.md)。

## <a name="is-there-a-newsgroup-for-umdf"></a>对于 UMDF 是否有新闻组？


您可以找到以下论坛上的 Windows 驱动程序的所有方面的讨论：

-   Microsoft 将维护[Windows 硬件 WDK 和驱动程序开发](http://social.msdn.microsoft.com/Forums/windowsdesktop/home?forum=wdk)论坛。

-   打开系统 Resources (OSR) 减少[OSR Online NTDEV 列表](http://www.osronline.com/showlists.cfm?list=ntdev)论坛。

 

 





