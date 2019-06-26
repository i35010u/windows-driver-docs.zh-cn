---
title: 查看 UMDF 对象
description: 本主题介绍如何使用 Wudfext.dll 调试器扩展，若要查看有关用户模式驱动程序框架 (UMDF) 版本 1 驱动程序使用的对象的信息。
ms.assetid: 36d0d604-3ed1-4ca7-b5bd-207942ecfc1e
keywords:
- WDK UMDF，查看 UMDF 对象的调试方案
- UMDF WDK，调试方案中，查看 UMDF 对象
- UMDF WDK，查看 UMDF 对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f723e30d418385b7f51bb8fdf3c619ce3507d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372157"
---
# <a name="viewing-umdf-objects"></a>查看 UMDF 对象

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

本主题介绍如何使用 Wudfext.dll 调试器扩展，若要查看有关用户模式驱动程序框架 (UMDF) 版本 1 驱动程序使用的对象的信息。

从 UMDF 版本 2 开始，应改为使用 Wdfkd.dll 调试器扩展。 有关详细信息，请参阅[Windows 驱动程序框架扩展 (Wdfkd.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。

您可以执行以下步骤来查看有关 UMDF 版本 1 对象的信息：

1.  使用以下 UMDF 调试器扩展插件之一来查看在主机进程的设备堆栈：
    -   **!wudfext.umdevstacks**
    -   **！ wudfext.umdevstack**如下面的示例中所示：

        **!wudfext.umdevstack &lt;dev-stack-addr&gt;**

        这些信息包括驱动程序对象和每个驱动程序的设备对象。 目前，UMDF 允许只有一个设备堆栈在主机进程中没有这两个扩展的输出之间没有差异。

2.  通过查看完整的对象树 **！ wudfext.wudfobject** UMDF 调试器扩展，如以下示例所示：

    **!wudfext.wudfobject &lt;IWDFDriver\*&gt; 1**

3.  使用 **！ wudfext.wudfdevice** UMDF 调试器扩展，如下面的示例以确定 Plug and Play (PnP) 和电源管理的设备状态中所示：

    **!wudfext.wudfdevice &lt;IWDFDevice\*&gt;**

4.  执行以下步骤来确定与设备关联的队列：
    1.  使用 **！ wudfext.wudfdevicequeues** UMDF 调试器扩展，以查看与设备相关联的队列。 此扩展会显示队列属性、 队列状态和驱动程序拥有的请求。
    2.  使用 **！ wudfext.wudfqueue** UMDF 调试器扩展，以获取有关每个队列的信息在下面的示例所示：

        **!wudfext.wudfqueue &lt;IWDFIoQueue\*&gt;**

5.  使用 **！ wudfext.wudfrequest** UMDF 调试器扩展，以获取有关特定请求的信息。 此信息包括基础用户模式下 I/O 请求数据包 (IRP)。 从用户模式下 IRP 信息，可以确定在其中请求当前正在处理在堆栈中。 此外可以使用 **！ wudfext.umirp** UMDF 调试器扩展来获取此用户模式下 IRP 信息。

6.  确定由所有 I/O 目标：

    1.  使用 **！ wudfext.wudfobject** UMDF 调试器扩展，若要查看的设备对象的子对象。 I/O 目标对象是设备对象的子对象。
    2.  使用 **！ wudfext.wudfiotarget** UMDF 调试器扩展，若要查看有关每个 I/O 目标对象的信息在下面的示例所示：

        **!wudfext.wudfiotarget &lt;IWDFTarget\*&gt;**

        此扩展显示的目标的状态和发送的请求数的列表。

    目前，可查看所有 I/O 目标没有 UMDF 调试器扩展。

7.  使用以下 UMDF 调试器扩展查看文件对象的信息：

    <a href="" id="-wudfext-wudfrequest-or--wudfext-umirp"></a> **！ wudfext.wudfrequest**或 **！ wudfext.umirp**  
    使用 **！ wudfext.wudfrequest**或 **！ wudfext.umirp** UMDF 调试器扩展是设备对象的子对象的视图文件。

    <a href="" id="-wudfext-wudffile"></a> **!wudfext.wudffile**  
    使用 **！ wudfext.wudffile** UMDF 调试器扩展，若要查看有关 framework 文件的信息在下面的示例所示：

    **!wudfext.wudffile &lt;IWDFFile\*&gt;**

    <a href="" id="-wudfext-umfile"></a> **!wudfext.umfile**  
    使用 **！ wudfext.umfile** UMDF 调试器扩展，如下面的示例中所示若要查看有关 UMDF 内部堆栈文件 （即文件堆栈中的驱动程序创建对象而不是由创建的文件对象的信息应用程序或由另一个堆栈中的驱动程序):

    **!wudfext.umfile &lt;addr&gt;**

    在某些情况下，可能不会有相应的框架文件，并且用户模式 IRP 信息可能包括 UMDF 内部堆栈文件。

    信息的 **！ wudfext.umfile**显示包括要排队发送至 UMDF 内部堆栈文件任何 Irp。 仅驱动程序创建的文件，跟踪对这些文件会排入队列的用户模式下 Irp。 对于应用程序创建的文件 I/O 管理器跟踪内核模式 Irp。

    <a href="" id="-wudfext-umdevstacks-and--wudfext-umdevstack"></a> **！ wudfext.umdevstacks**和 **！ wudfext.umdevstack**  
    使用的输出 **！ wudfext.umdevstacks**并 **！ wudfext.umdevstack** UMDF 调试器扩展，若要查看与驱动程序创建文件相对应的未完成 UMDF 内部堆栈文件。

 

 





