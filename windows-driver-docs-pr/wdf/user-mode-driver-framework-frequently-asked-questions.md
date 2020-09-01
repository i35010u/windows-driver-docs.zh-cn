---
title: 用户模式驱动程序框架常见问题解答
description: Windows 驱动程序框架 (WDF) 是一组可用于编写在 Windows 操作系统上运行的设备驱动程序的库。
ms.assetid: 0c07e514-73f9-4d24-86ad-8ac036fdbcf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f595c738d7e4b6b3b22882195174b7b25a6c8b41
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187323"
---
# <a name="user-mode-driver-framework-frequently-asked-questions"></a>用户模式驱动程序框架常见问题解答


Windows 驱动程序框架 (WDF) 是一组可用于编写在 Windows 操作系统上运行的设备驱动程序的库。 WDF 定义了两个框架支持的单个驱动程序模型：内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 。 本主题提供有关 UMDF 的常见问题的解答。

## <a name="which-operating-systems-can-run-umdf-drivers"></a>哪些操作系统可以运行 UMDF 驱动程序？


你可以在以下操作系统上运行 UMDF 驱动程序：

-   Windows 10
-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista
-   Windows XP

## <a name="what-is-the-most-recent-version-of-umdf"></a>最新版本的 UMDF 是什么？


2.0 和 2.1) 的 UMDF 版本 2 (都包含在 Windows 10 和更高版本中。

## <a name="what-is-the-difference-between-umdf-version-2-and-the-previous-version-111-one-dot-eleven"></a>UMDF 版本2和上一版本之间的区别是，1.11 (一个点十一) ？


用 UMDF 版本2编写的驱动程序以 C 编程语言编写。 然后，可以轻松地为 KMDF 编译此同一个驱动程序。 此外，必须根据 COM 编程模型写入 UMDF 版本1驱动程序。 

有关详细信息，请参阅 [具有 UMDF 的入门](getting-started-with-umdf-version-2.md)。

## <a name="which-operating-systems-support-umdf-2"></a>哪些操作系统支持 UMDF 2？


UMDF 版本2驱动程序在 Windows 8.1 和更高版本上运行。

## <a name="which-umdf-versions-can-i-build-against-in-windows-driver-kit-wdk10"></a>我可以在 Windows 驱动程序工具包中构建哪些 UMDF 版本 (WDK) 10？


你可以使用 Windows 驱动程序工具包，使用 Windows 驱动程序 (工具包生成 UMDF 2.1、2.0、1.11 和1.9 驱动程序) 10 和 Microsoft Visual Studio。 有关哪些版本的 Windows 可以运行使用这些 UMDF 版本生成的驱动程序的信息，请参阅 [UMDF 版本历史记录](umdf-version-history.md)。

## <a name="can-i-write-part-of-my-driver-to-run-in-user-mode-and-part-in-kernel-mode"></a>我是否可以编写部分的驱动程序以在用户模式下运行，并在内核模式下运行？


是的。 即使您的驱动程序需要访问某些内核模式资源或功能，您也可以将您的驱动程序拆分为两个部分。 利用此方法，你可以受益于在用户模式下开发和运行驱动程序的一些优点。

UMDF 驱动程序可以接收来自内核模式驱动程序的 i/o 请求。 有关 *内核模式客户端*的详细信息，请参阅 [在 UMDF 2 驱动程序中支持内核模式客户端](supporting-kernel-mode-clients-in-umdf-drivers.md)。

然而，在 KMDF 和 UMDF 之间增加了奇偶校验，你几乎不需要拆分驱动程序。

##  <a name="which-framework-should-i-start-with"></a>应该从哪个框架开始？


如果你的驱动程序需要将 [UMDF 2 功能与 KMDF 进行比较](comparing-umdf-2-0-functionality-to-kmdf.md)的常用功能，则必须使用 KMDF。 对于所有其他驱动程序，您的第一个选择应该是 UMDF。

如果开始使用 UMDF，并决定稍后过渡到 KMDF，可以使用最少的工作量完成此操作，如 [如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序 (，反之亦然) ](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。

## <a name="how-do-user-mode-drivers-handle-security"></a>用户模式驱动程序如何处理安全性？


UMDF 驱动程序在驱动程序主机进程中运行，该进程在 LocalService 帐户的安全凭据中运行，尽管主机进程本身不是 Windows 服务。 因此，用户模式驱动程序与任何其他用户模式服务一样安全。 当 UMDF 驱动程序发出 i/o 请求时，它可以选择性地模拟它的客户端进程。 模拟使得驱动程序线程能够在客户端的安全上下文中运行，以便系统对客户端的标识（而不是驱动程序主机进程）执行访问检查。

用户模式驱动程序只能模拟 i/o 请求的客户端进程，而不能模拟即插即用或其他系统消息的客户端进程。

安装驱动程序时，INF 文件会为驱动程序设置最大的模拟级别。 模拟应在尽可能低的级别进行设置，以防止 "特权提升" 攻击。 当客户端应用程序调用 **CreateFile** 函数时，它将指定模拟级别。 然后，该驱动程序将针对每个单个 i/o 请求请求此级别的模拟。

## <a name="will-a-user-mode-driver-be-fast-enough"></a>用户模式驱动程序的速度是否足够快？


在开发 UMDF 时，性能非常重要。 尽管延迟和 CPU 使用率都在某种程度上增加，但总线容量是适用于 UMDF 支持的设备类型的主要门因数。

## <a name="what-is-the-difference-between-a-user-mode-driver-and-an-application"></a>用户模式驱动程序和应用程序之间的区别是什么？


用户模式驱动程序由驱动程序管理器启动，并在驱动程序主机进程中运行。 驱动程序的单个实例可以同时处理来自多个应用程序的请求。 为了与驱动程序通信，应用程序会通过 Win32 API 向驱动程序的设备发出 i/o 请求。 用户模式驱动程序中的主要入口点是 (UMDF 1.11 及更早版本) 或[**DriverEntry**](./driverentry-for-kmdf-drivers.md)例程的[**IDriverEntry**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)接口， (从 umdf 2.0) 开始，而不是从**主 ( # B5**函数开始。

驱动程序还包括为响应 i/o 请求和即插即用和电源通知而调用的附加接口或回调。 由 UMDF 驱动程序管理的设备集成到系统中，并参与即插即用和电源管理。

## <a name="how-do-i-debug-a-umdf-driver"></a>如何实现调试 UMDF 驱动程序？


可以使用用户模式调试器或内核模式调试程序调试 UMDF 驱动程序。 有关详细信息，请参阅 [调试 WDF 驱动程序](debugging-a-wdf-driver.md)。

从 UMDF 版本2.0 开始，可以使用 *Wdfkd.dll* 调试程序扩展库中的许多命令来调试 UMDF 驱动程序。 有关命令列表，请参阅 [调试器扩展](debugger-extensions-for-kmdf-drivers.md)。 此外，UMDF 还会在内核非分页内存中存储 UMDF 跟踪日志 (或 UMDF *IFR*) 。 有关 IFR 的信息，请参阅 [使用框架的事件记录器](using-the-framework-s-event-logger.md)。

## <a name="is-there-a-newsgroup-for-umdf"></a>是否有用于 UMDF 的新闻组？


您可以在以下论坛上找到有关 Windows 驱动程序的所有方面的讨论：

-   Microsoft 维护 [Windows 硬件 WDK 和驱动程序开发](https://social.msdn.microsoft.com/Forums/windowsdesktop/home?forum=wdk) 论坛。

-   打开 "系统资源" (OSR) moderates [OSR ONLINE NTDEV List](https://community.osr.com/) 论坛。

 

