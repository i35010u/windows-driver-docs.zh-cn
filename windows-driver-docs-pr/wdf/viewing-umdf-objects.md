---
title: 查看 UMDF 对象
description: 本主题介绍如何使用 Wudfext 调试器扩展来查看有关用户模式驱动程序框架（UMDF）版本1驱动程序所使用的对象的信息。
ms.assetid: 36d0d604-3ed1-4ca7-b5bd-207942ecfc1e
keywords:
- 调试方案 WDK UMDF，查看 UMDF 对象
- UMDF WDK，调试方案，查看 UMDF 对象
- UMDF WDK，查看 UMDF 对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef76bb5911a3c447150025eef1158b594d1502e6
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210855"
---
# <a name="viewing-umdf-objects"></a>查看 UMDF 对象

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

本主题介绍如何使用 Wudfext 调试器扩展来查看有关用户模式驱动程序框架（UMDF）版本1驱动程序所使用的对象的信息。

从 UMDF 版本2开始，你应该改用 Wdfkd 调试器扩展。 有关详细信息，请参阅[Windows 驱动程序框架扩展（Wdfkd）](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。

你可以执行以下步骤来查看有关 UMDF 版本1对象的信息：

1.  使用下列 UMDF 调试器扩展之一来查看主机进程中的设备堆栈：
    -   **!wudfext.umdevstacks**
    -   **！ wudfext umdevstack** ，如以下示例中所示：

        **！ wudfext&gt; &lt;开发堆栈-地址**

        此信息包括每个驱动程序的驱动程序对象和设备对象。 目前，UMDF 只允许在一个主机进程中使用一个设备堆栈，因此这两个扩展的输出没有任何区别。

2.  使用 **！ wudfext** ，查看完整的对象树，如以下示例中所示：

    **！ wudfext. wudfobject &lt;IWDFDriver\*&gt; 1**

3.  如以下示例中所示，使用 **！ wudfext wudfdevice** UMDF 调试器扩展来确定设备的即插即用（PnP）和电源管理状态：

    **！ wudfext. wudfdevice &lt;IWDFDevice\*&gt;**

4.  执行以下步骤以确定与设备关联的队列：
    1.  使用 **！ wudfext wudfdevicequeues** UMDF 调试器扩展来查看与设备关联的队列。 此扩展显示队列属性、队列状态和驱动程序拥有的请求。
    2.  如以下示例中所示，使用 **！ wudfext wudfqueue** UMDF 调试器扩展来获取有关每个队列的信息：

        **！ wudfext. wudfqueue &lt;IWDFIoQueue\*&gt;**

5.  使用 **！ wudfext wudfrequest** UMDF 调试器扩展来获取有关特定请求的信息。 此信息包括基础用户模式 i/o 请求数据包（IRP）。 通过用户模式 IRP 信息，你可以确定当前在堆栈中处理请求的位置。 你还可以使用 **！ wudfext umirp** UMDF 调试器扩展来获取此用户模式的 IRP 信息。

6.  通过以下方式确定所有 i/o 目标：

    1.  使用 **！ wudfext. wudfobject** UMDF 调试器扩展来查看 device 对象的子对象。 I/o 目标对象是 device 对象的子对象。
    2.  如以下示例中所示，使用 **！ wudfext wudfiotarget** UMDF 调试器扩展来查看有关每个 i/o 目标对象的信息：

        **！ wudfext. wudfiotarget &lt;IWDFTarget\*&gt;**

        此扩展显示目标的状态和已发送请求的列表。

    当前没有可用于查看所有 i/o 目标的 UMDF 调试器扩展。

7.  使用以下 UMDF 调试器扩展查看有关文件对象的信息：

    <a href="" id="-wudfext-wudfrequest-or--wudfext-umirp"></a>**！ wudfext. wudfrequest**或 **！ wudfext umirp**  
    使用 **！ wudfext; wudfrequest**或**umirp** UMDF 调试器扩展来查看作为设备对象的子对象的文件。

    <a href="" id="-wudfext-wudffile"></a>**!wudfext.wudffile**  
    如以下示例中所示，使用 **！ wudfext wudffile** UMDF 调试器扩展来查看有关框架文件的信息：

    **！ wudfext. wudffile &lt;IWDFFile\*&gt;**

    <a href="" id="-wudfext-umfile"></a>**!wudfext.umfile**  
    如以下示例中所示，使用 **！ wudfext umfile** UMDF 调试器扩展来查看有关 UMDF 堆栈内文件（即，堆栈中的驱动程序所创建的文件对象，而不是由应用程序创建的文件对象或另一堆栈中的驱动程序所创建的文件对象）的信息：

    **！ wudfext. umfile &lt;地址&gt;**

    在某些情况下，可能没有对应的框架文件，并且用户模式 IRP 信息可能包含 UMDF 堆栈内文件。

    **！ Wudfext umfile**显示的信息包含排队到 UMDF 堆栈内文件的任何 irp。 只有驱动程序创建的文件跟踪排队到这些文件的用户模式 Irp。 对于应用程序创建的文件，i/o 管理器跟踪内核模式 Irp。

    <a href="" id="-wudfext-umdevstacks-and--wudfext-umdevstack"></a>**！ wudfext. umdevstacks** and **！ wudfext. umdevstack**  
    使用 **！ wudfext**和 **！ wudfext. umdevstack** UMDF 调试器扩展的输出来查看与驱动程序创建的文件相对应的未处理 UMDF 堆栈内文件。

 

 





