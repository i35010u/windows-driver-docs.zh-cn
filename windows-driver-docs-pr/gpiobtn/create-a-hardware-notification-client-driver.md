---
title: 创建硬件通知客户端驱动程序
description: 本部分提供使用 KMDF 类扩展由 Microsoft 提供的硬件通知客户端驱动程序的开发的常规指南。
ms.assetid: 348950d3-fb80-4800-a606-290d473aa412
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ef6f9d7653241245c1c462bb008cfc2a766bef36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576907"
---
# <a name="create-a-hardware-notification-client-driver"></a>创建硬件通知客户端驱动程序


本部分提供使用 KMDF 类扩展由 Microsoft 提供的硬件通知客户端驱动程序的开发的常规指南。

1.  创建链接到 Mshwnclxstub.lib 以及包含标头 hwn.h 和 hwnclx.h 根据客户端驱动程序实现的文件。

2.  定义所需 KMDF 和硬件通知类扩展回调的函数的实例。 具体而言，必须实现和注册这些回调函数，如下面的代码示例中所示。

    ```cpp
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD HwnClientEvtDeviceAdd;
    HWN_CLIENT_INITIALIZE_DEVICE HwnClientInitializeDevice;
    HWN_CLIENT_UNINITIALIZE_DEVICE HwnClientUnInitializeDevice;
    HWN_CLIENT_QUERY_DEVICE_INFORMATION HwnClientQueryDeviceInformation;
    HWN_CLIENT_START_DEVICE HwnClientStartDevice;
    HWN_CLIENT_STOP_DEVICE HwnClientStopDevice;
    HWN_CLIENT_SET_STATE HwnClientSetState;
    HWN_CLIENT_GET_STATE HwnClientGetState;
    ```

3.  实现[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，它是客户端驱动程序入口点，负责初始化。 硬件通知客户端驱动程序，此函数应处理以下：

    -   调用[ **WDF\_驱动程序\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff551302)若要初始化的驱动程序[ **WDF\_驱动程序\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)结构。

    -   调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)创建客户端驱动程序的框架驱动程序对象。

    -   定义的内容[ **HWN\_客户端\_注册\_数据包**](https://msdn.microsoft.com/library/windows/hardware/mt843560)，通过此类扩展包括使用的回调函数指针。 有关必需的回调函数的详细信息，请参阅[硬件通知引用](https://msdn.microsoft.com/library/windows/hardware/dn789336)。

    -   调用[HwNRegisterClient](https://msdn.microsoft.com/library/windows/hardware/mt843550)将客户端驱动程序注册到此类扩展。

4.  实现[ *EVT\_WDF\_驱动程序\_设备\_添加*](https://msdn.microsoft.com/library/windows/hardware/ff541693)函数，这是负责执行设备初始化操作当 PnP 管理器报告设备是否的存在。 硬件通知客户端驱动程序，此函数应处理以下：

    -   调用[ **HwNProcessAddDevicePreDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/mt843549)，提供设备的准备/发行版和入口/出口回调，KMDF 需转换为各状态的设备。

    -   调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)创建 framework 设备对象。

    -   调用[ **HwNProcessAddDevicePostDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt843548)创建 I/O 队列。

5.  实现定义[ **HWN\_客户端\_初始化\_设备**](https://msdn.microsoft.com/library/windows/hardware/mt843553)类扩展来准备硬件通知调用的函数使用控制器。

6.  实现定义[ **HWN\_客户端\_UNINITIALIZE\_设备**](https://msdn.microsoft.com/library/windows/hardware/mt827292)函数调用的类扩展取消初始化硬件通知控制器。

7.  实现定义[ **HWN\_客户端\_查询\_设备\_信息**](https://msdn.microsoft.com/library/windows/hardware/mt843554)类扩展调用的函数。 此函数负责检索硬件通知组件的属性。

8.  实现定义[ **HWN\_客户端\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/mt843557)类扩展调用的函数。 此函数是负责启动硬件通知控制器，并为客户端驱动程序分配 ACPI 的资源。

9.  实现定义[ **HWN\_客户端\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/mt843558)类扩展调用的函数。 此函数是负责停止硬件通知控制器，并释放 ACPI 资源使用的客户端驱动程序。

10. 实现定义[ **HWN\_客户端\_设置\_状态**](https://msdn.microsoft.com/library/windows/hardware/mt843556)，调用此类扩展。 此函数负责设置硬件通知组件状态。

11. 实现定义[ **HWN\_客户端\_获取\_状态**](https://msdn.microsoft.com/library/windows/hardware/mt843552)，调用此类扩展。 此函数负责获取硬件通知组件的当前值。 当输入的缓冲区为 NULL，这意味着用户未指定特定硬件通知状态，此函数应返回的所有硬件通知组件的状态信息。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[硬件通知](hardware-notifications-support.md)

[硬件通知参考](https://msdn.microsoft.com/library/windows/hardware/dn789336)



