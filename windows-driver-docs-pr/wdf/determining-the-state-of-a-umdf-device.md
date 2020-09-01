---
title: 确定 UMDF 设备的状态
description: 本主题介绍如何将调试程序扩展与用户模式驱动程序框架结合使用， (UMDF) 版本1或2驱动程序，以确定 UMDF 设备处于何种状态。
ms.assetid: ed1a4429-4f36-44b9-9564-587aa381342f
keywords:
- UMDF WDK，UMDF 设备状态
- UMDF WDK，设备状态
- 用户模式调试器 WDK UMDF，确定 UMDF 设备状态
- 内核模式调试程序 WDK UMDF，确定 UMDF 设备状态
- 调试方案 WDK UMDF，UMDF 设备状态
- UMDF WDK，调试方案，UMDF 设备状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 203ec3f5bbe9b623c03ce9624e4df39ffa250d6f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191562"
---
# <a name="determining-the-state-of-a-umdf-device"></a>确定 UMDF 设备的状态


本主题介绍如何将调试程序扩展与用户模式驱动程序框架结合使用， (UMDF) 版本1或2驱动程序，以确定 UMDF 设备处于何种状态。

对于 UMDF 版本1，你将使用在 wudfext.dll 中实现的扩展命令。 从 UMDF 版本2开始，你将使用在 wdfkd.dll 中实现的扩展命令。

若要确定设备状态，请使用以下步骤：

1.  使用以下一种调试器类型分解为驱动程序主机进程：
    -   用户模式调试器：
        1.  查找设备 (的相应驱动程序主机进程，WUDFHost.exe) "。 如果有多个主机进程实例，则可以使用操作系统提供的 Tasklist.exe 应用程序来确定哪个进程承载了驱动程序。

            在提升的命令提示符中使用此命令。

            **tasklist-m &lt;yourdriver.dll&gt;**

        2.  通过提升的权限启动调试器，并附加到相应的进程。
        3.  使用 **reload.sql 调试器命令** 重新加载符号。
        4.  可以通过使用** ~ \* k**调试器命令查看所有线程。

    -   内核模式调试器：
        1.  查找设备 (的相应驱动程序主机进程，WUDFHost.exe) "。 使用 **！处理** 内核模式调试程序扩展，如以下示例中所示，以获取所有 WUDFHost.exe 实例的列表：

            **！进程 0 0 WUDFHost.exe**

            在后续步骤中，将使用来自 **！ process 0 0** 输出的进程地址和进程环境块 (PEB) 地址。

        2.  通过以下方式之一附加到主机进程：
            -   对于非侵害性连接，请使用 **. process** 调试器命令，如以下示例中所示：

                **。 process/p/r &lt; 进程-地址&gt;**

                如果不允许继续执行，则应使用非侵害性连接。 例如，如果你在应用程序中收到中断，并且想要查看驱动程序执行中断的原因或反射器准备终止宿主进程，则应使用非侵害性连接。

            -   在侵害性连接中使用 **. process** 调试器命令，如以下示例中所示：

                **。进程/i &lt; 进程-地址&gt;**

                调试器将请求你使用 **g** 调试器命令继续操作;执行 **g** 调试器命令后，调试器将进入活动进程。 使用以下示例中所示的 **reload.sql** 调试器命令重载用户符号：

                **。重新加载/user**

        3.  如果有多个主机进程实例，则可以使用以下示例中所示的 **！ peb** general 调试器扩展来获取进程中加载的模块的列表：

            **！ peb &lt; peb-Address&gt;**

            需要附加到进程，此命令才能工作。 可以附加非 invasively，如前一步骤中所示。

            找到加载驱动程序 DLL 的进程。

        4.  使用 **！进程** 内核模式调试程序扩展，如以下示例中所示，以获取有关进程的信息。 此信息包括进程中运行的线程以及这些线程的地址：

            **！进程 &lt; 进程-地址&gt;**

        5.  使用 **！线程** 内核模式调试器扩展，如以下示例中所示，获取有关每个线程的信息：

            **！线程 &lt; 线程-地址&gt;**

2.  在调试器中，使用 **链式** 命令查看是否加载了 wudfext.dll (umdf 1) 或 wdfkd.dll (umdf 2) 调试器扩展库。
3.  如果需要的库不存在，请使用 [**load**](../debugger/-load---loadby--load-extension-dll-.md) 命令将扩展 DLL 加载到调试器中。 然后输入 **，** 重新加载符号信息。
4.  使用 [**！ wudfext，**](../debugger/-wudfext-umdevstacks.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfumdevstacks.md) (umdf 2) 查看主机进程中加载的所有设备堆栈。

    然后，使用 [**！ wudfext. umdevstack**](../debugger/-wudfext-umdevstack.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfumdevstack.md) (umdf 2) 获取有关设备堆栈的详细信息。

5.  使用 [**！ wudfext. wudfdevice**](../debugger/-wudfext-wudfdevice.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfdevice.md) (UMDF 2) 获取有关设备即插即用 (PnP) 和电源管理状态的信息。

6.  使用 [**！ wudfext**](../debugger/-wudfext-wudfdriverinfo.md) ， (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfdriverinfo.md) (umdf 2) 以显示有关该驱动程序的其他信息，包括其设备树。

 

