---
title: 编写 UMDF 驱动程序的优点
description: 本主题介绍编写 User-Mode Driver Framework (UMDF) 驱动程序而不是内核模式驱动程序的优点。
keywords:
- User-Mode Driver Framework WDK，优点
- UMDF WDK，优点
- 用户模式驱动程序 WDK UMDF，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 423ac9f9a75de511b73149064c3ac4c4ccbc715d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815791"
---
# <a name="advantages-of-writing-umdf-drivers"></a>编写 UMDF 驱动程序的优点


本主题介绍编写 User-Mode Driver Framework (UMDF) 驱动程序而不是内核模式驱动程序的优点。

写入 UMDF 驱动程序时，将从以下内容受益：

-   UMDF 驱动程序会导致更高的操作系统稳定性，因为它们只能访问运行它们的进程的地址空间。
-   因为 UMDF 驱动程序在 **LocalService** 帐户下运行，所以它们对用户的数据或系统文件具有有限的访问权限。
-   用户模式驱动程序在比内核模式驱动程序更简单的环境中运行。 例如，内核模式驱动程序必须考虑到 IRQL、页面错误和线程上下文。 但在用户模式下，这些问题并不存在。 用户模式驱动程序始终在来自请求进程的不同线程中运行，并且始终可以获取页面错误。

-   UMDF 版本2在大多数区域中提供 KMDF 的功能奇偶校验。 有关完整比较，请参阅 [将 UMDF 2 功能与 KMDF 进行比较](comparing-umdf-2-0-functionality-to-kmdf.md)。
-   UMDF 版本2有助于在 KMDF 和 UMDF 之间转换。 请参阅 [如何 (将 KMDF 驱动程序转换为 UMDF 2 驱动程序，反之亦然) ](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。
-   您可以通过使用用户模式调试器，或从 UMDF 版本2（内核模式调试程序）开始调试 UMDF 驱动程序。

-   可以通过 KMDF 使用 Wdfkd.dll 调试程序扩展命令，并从 UMDF 版本2开始。 有关详细信息，请参阅 [调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

总体 WDF 模型的基本目标是提供智能默认值，以便您可以专注于设备硬件，并避免编写代码来执行大多数驱动程序所共有的任务。

为了实现此目标，该框架旨在与 "选择加入" 的驱动程序一起使用。 写入 UMDF 驱动程序时，仅为影响设备的事件提供回调例程。 例如，某些设备在开机后以及在关闭之前都需要立即进行干预。 此类设备的驱动程序可以实现框架在这些时间调用的回调函数。

驱动程序包括仅处理其设备需要特定于设备的支持的事件的代码。 所有其他事件都可以通过框架默认值进行处理。

此外，驱动程序可以配置其 i/o 请求队列，以便在设备处于低功耗状态时停止调度请求，并在设备恢复到操作状态后恢复调度。 同样，如果 i/o 请求在设备处于低功耗状态时到达，则框架可以自动打开设备。

 

 





