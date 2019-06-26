---
title: 确定 UMDF 设备的状态
description: 本主题介绍如何结合使用用户模式驱动程序框架 (UMDF) 版本 1 或 2 驱动程序中使用调试器扩展来确定 UMDF 设备处于什么状态。
ms.assetid: ed1a4429-4f36-44b9-9564-587aa381342f
keywords:
- UMDF WDK，UMDF 设备状态
- UMDF WDK，设备状态
- 用户模式下的调试器 WDK UMDF，确定 UMDF 设备状态
- 内核模式调试器 WDK UMDF，确定 UMDF 设备状态
- 调试方案 WDK UMDF UMDF 设备状态
- UMDF WDK，调试方案，UMDF 设备状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31efec7ebf074d7c67b153a95c7509bdf36036a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377443"
---
# <a name="determining-the-state-of-a-umdf-device"></a>确定 UMDF 设备的状态


本主题介绍如何结合使用用户模式驱动程序框架 (UMDF) 版本 1 或 2 驱动程序中使用调试器扩展来确定 UMDF 设备处于什么状态。

对于 UMDF 版本 1，将使用在 wudfext.dll 中实现的扩展命令。 从 UMDF 版本 2 开始，将使用在 wdfkd.dll 中实现的扩展命令。

若要确定设备状态，请使用以下步骤：

1.  分解为驱动程序主机进程，使用以下调试器类型之一：
    -   用户模式下的调试器：
        1.  找到设备 (即，WUDFHost.exe) 的相应的驱动程序主机进程。 如果有多个实例的主机进程，可以使用操作系统提供 Tasklist.exe 应用程序以确定哪个进程正在承载您的驱动程序。

            使用此命令从提升的命令提示符。

            **tasklist -m &lt;yourdriver.dll&gt;**

        2.  使用提升的特权启动调试器并附加到相应的进程。
        3.  使用重新加载符号 **.reload**调试器命令。
        4.  可以通过查看所有线程 **~ \*k**调试器命令。

    -   内核模式调试程序：
        1.  找到设备 (即，WUDFHost.exe) 的相应的驱动程序主机进程。 使用 **！ 过程**内核模式调试程序扩展来获取所有 WUDFHost.exe 实例的列表，在下面的示例所示：

            **！ process 0 0 WUDFHost.exe**

            进程地址并从进程环境块 (PEB) 地址 **！ process 0 0**输出在后续步骤中使用。

        2.  附加到主机进程中的以下方法之一：
            -   使用 **.process**调试器命令，以便非入侵性附加，如以下示例所示：

                **.process /p /r &lt;process-addr&gt;**

                应使用非入侵性附加时不能允许继续执行。 例如，您应使用非入侵性时在应用程序中接收一个分行符和你想要查看该发送程序准备终止主机进程时或若要使该中断驱动程序未附加。

            -   使用 **.process**中侵入性的调试器命令附加在下面的示例所示：

                **.process /i &lt;process-addr&gt;**

                调试器将请求继续使用**g**调试器命令; 在执行后不久**g**调试器命令时，调试器将中断并进入活动的进程。 使用重新加载用户符号 **.reload**调试器命令，如以下示例中所示：

                **.reload /user**

        3.  如果有多个实例的主机进程，则可以使用 **！ peb**常规调试器扩展来获取进程中加载的模块列表在下面的示例所示：

            **!peb &lt;PEB-Address&gt;**

            您需要将附加到使用此命令的过程。 你可以附加非-invasively 上一步中所示。

            找到您的驱动程序 DLL 加载中的进程。

        4.  使用 **！ 过程**内核模式调试程序扩展，以获取有关过程的信息在下面的示例所示。 信息包括在该过程和这些线程的地址中运行的线程：

            **!process &lt;process-addr&gt;**

        5.  使用 **！ 线程**内核模式调试程序扩展，以获取有关每个线程的信息在下面的示例所示：

            **!thread &lt;thread-addr&gt;**

2.  在调试器中，使用 **.chain**命令来查看加载 wudfext.dll (UMDF 1) 或 wdfkd.dll (UMDF 2) 调试器扩展库。
3.  如果不存在所需的库，请使用[ **.load** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-load---loadby--load-extension-dll-)命令来扩展 DLL 加载到调试器。 然后输入 **.reload**以重新加载符号信息。
4.  使用[ **！ wudfext.umdevstacks** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umdevstacks) (UMDF 1) 或[ **！ wdfkd.wdfumdevstacks** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks) (UMDF 2) 若要查看所有设备堆栈在主机进程中加载。

    然后，使用[ **！ wudfext.umdevstack** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umdevstack) (UMDF 1) 或[ **！ wdfkd.wdfumdevstack** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack) (UMDF 2) 若要获取有关设备的详细的信息堆栈。

5.  使用[ **！ wudfext.wudfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdevice) (UMDF 1) 或[ **！ wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice) (UMDF 2) 若要获取有关 Plug and Play (PnP) 的信息和电源管理的设备的状态。

6.  使用[ **！ wudfext.wudfdriverinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdriverinfo) (UMDF 1) 或[ **！ wdfkd.wdfdriverinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo) (UMDF 2)，以显示有关其他信息驱动程序，包括其设备树。

 

 





