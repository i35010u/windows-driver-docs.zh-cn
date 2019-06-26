---
title: UMDF 如何处理驱动程序故障
description: 本主题介绍用户模式驱动程序框架 (UMDF) 和操作系统 UMDF 驱动程序失败时执行的操作。 它适用于这两种 UMDF 版本 1 和 2。
ms.assetid: 1811f131-6a51-4e53-bc8d-da511619f6fd
keywords:
- 用户模式驱动程序框架 WDK，驱动程序失败
- UMDF WDK，驱动程序失败
- 用户模式驱动程序 WDK UMDF，驱动程序失败
- 失败的驱动程序 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a7ea0e4fcb927bdb8d1e77f1bcd5bdc638f9eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382836"
---
# <a name="how-umdf-handles-driver-failures"></a>UMDF 如何处理驱动程序故障


本主题介绍用户模式驱动程序框架 (UMDF) 和操作系统 UMDF 驱动程序失败时执行的操作。 它适用于这两种 UMDF 版本 1 和 2。

按以下顺序发生以下事件：

-   操作系统会通知该发送程序 (*WUDFRd.sys*)。

-   该发送程序跟踪的主机进程中的未完成 i/o 操作：
    -   反射器完成未完成 i/o 操作的状态\_驱动程序\_进程\_已终止错误代码。
    -   Microsoft Win32 应用程序收到错误消息\_驱动程序\_进程\_已终止未完成 i/o 操作的错误代码。

    **请注意**  在 Microsoft Windows XP 运行该发送程序完成状态为未完成 I/O\_驱动程序\_内部\_错误，Win32 应用程序，反过来，收到错误\_IO\_针对未完成 I/O 设备错误代码。 因此，在 Windows XP 运行的应用程序不应使用错误\_IO\_设备检测驱动程序失败，因为它们不能确定从一个典型的 I/O 请求 （例如，状态返回的状态的任何差异返回通过调用 Win32 [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数)。

     

-   该发送程序将发送 GUID\_WUDF\_设备\_主机\_问题到操作系统后，操作系统报告的问题与宿主进程的自定义和插即用 (PnP) 事件。

    如果应用程序以前称为 Win32 **RegisterDeviceNotification**函数以注册 GUID\_WUDF\_设备\_主机\_设备，该应用程序的问题将收到 DBT\_CUSTOMEVENT 通知时的宿主进程将失败。 有关详细信息**RegisterDeviceNotification**和 DBT\_CUSTOMEVENT，请参阅 Windows SDK 文档。

-   操作系统将条目写入到系统事件日志，该值指示此驱动程序失败。 它还指示多少操作系统的更多时间将重新启动该驱动程序。 操作系统将下面的事件编号，写入到系统事件日志，以表示指定的问题：

    -   如果主机进程错误而引起的 10110
    -   如果设备处于脱机并重新启动，10111
    -   10112 如果设备处于脱机和未重新启动

    该框架可以尝试重新启动失败驱动程序。 UMDF 代码验证程序提供了[注册表值](using-umdf-verifier.md)控制重新启动尝试次数。 如果用户是禁用和启用设备在设备管理器或断开并插入设备，操作系统会创建该设备的新实例并框架将重启计数器重置。

-   操作系统卸载设备堆栈中的内核驱动程序。

    **请注意**  操作系统将不关闭并重新启动设备堆栈，直到旧堆栈的所有句柄已关闭。 应用程序将检测设备故障和意外删除通知设备 (DBT\_REMOVEDEVICEPENDING)。 但是，如果任何句柄旧堆栈保持打开状态，将不重启设备。

     

-   驱动程序管理器重新启动，或禁用设备。 如果禁用设备，则操作系统会显示一个黄色感叹号设备管理器中。

请注意，UMDF 驱动程序失败后，发生以下操作可以按任意顺序：

-   操作系统关闭并重新启动设备。

-   该发送程序将发送 GUID\_WUDF\_设备\_主机\_问题对操作系统的即插即用事件。

-   反射器完成状态为未完成 I/O\_驱动程序\_进程\_已终止。

因此，应用程序可能会收到错误\_驱动程序\_进程\_操作系统重新启动设备后终止对未完成 i/o 操作。 收到错误后\_驱动程序\_进程\_终止，该应用程序还可能会收到 DBT\_GUID 而得出的 CUSTOMEVENT 通知\_WUDF\_设备\_主机\_问题事件。

 

 





