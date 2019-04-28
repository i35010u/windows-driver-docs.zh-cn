---
title: 编写 UMDF 驱动程序的优点
description: 本主题介绍编写而不是内核模式驱动程序的用户模式驱动程序框架 (UMDF) 驱动程序的优点。
ms.assetid: 28db2121-a5d4-4375-8081-52709416efb0
keywords:
- 用户模式驱动程序框架 WDK 优点
- UMDF WDK 优点
- 用户模式驱动程序 WDK UMDF，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355d215fb633b51e6e629833ab7fb8699963b0bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350726"
---
# <a name="advantages-of-writing-umdf-drivers"></a>编写 UMDF 驱动程序的优点


本主题介绍编写而不是内核模式驱动程序的用户模式驱动程序框架 (UMDF) 驱动程序的优点。

在编写 UMDF 驱动程序时，将从以下受益：

-   UMDF 驱动程序导致更高版本操作系统的稳定性，因为它们具有访问权限仅对其运行进程的地址空间。
-   因为 UMDF 驱动程序下运行**LocalService**帐户，具有有限的访问用户的数据或系统文件。
-   用户模式驱动程序运行在更简单环境比内核模式驱动程序中。 例如，内核模式驱动程序必须考虑到帐户的 IRQL、 页面错误和线程上下文。 在用户模式下，但是，这些问题不存在。 用户模式驱动程序始终在请求过程中的不同线程中运行，并始终采用页面错误。

-   UMDF 版本 2 提供了 KMDF 大多数区域中的功能奇偶一致性。 有关完整比较，请参阅[比较 UMDF 2 功能提供给 KMDF](comparing-umdf-2-0-functionality-to-kmdf.md)。
-   UMDF 版本 2 便于 KMDF 和 UMDF 之间进行转换。 请参阅[如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序 （和进行相反转换）](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。
-   可以通过使用用户模式下调试器，或从 UMDF 版本 2，内核模式调试程序调试 UMDF 驱动程序。

-   使用 KMDF 和 UMDF 版本 2 开始，可以使用 Wdfkd.dll 调试器扩展命令。 有关详细信息，请参阅[调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

总体 WDF 模型的重要目标是提供智能默认值，以便可以专注于你设备的硬件和编写代码来执行任务所共有的大多数驱动程序。

若要实现此目标，框架设计用于处理一次"参加"，按照上的驱动程序。 当您编写 UMDF 驱动程序时，只会影响你的设备的事件提供回调例程。 例如，某些设备需要干预，立即在开启之后，只需之前关闭了。 此类设备的驱动程序可以实现在这些时间框架将调用的回调函数。

该驱动程序包含用于处理其设备为其需要特定于设备的支持这些事件的代码。 由框架的默认值，可以处理所有其他事件。

此外，驱动程序可以配置其 I/O 请求队列，以便在 framework 停止当设备在低功耗状态并恢复调度后设备返回到操作状态时，将请求发送。 同样，如果设备处于低功耗状态时，I/O 请求到达时，框架可以自动打开设备。

 

 





