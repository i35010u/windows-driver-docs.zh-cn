---
title: 创建硬件通知客户端驱动程序
description: 本部分提供了有关如何开发使用 Microsoft 提供的 KMDF 类扩展的硬件通知客户端驱动程序的一般指南。
ms.assetid: 348950d3-fb80-4800-a606-290d473aa412
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2b1d1b931de07e456a7249f66b33b0b5b6b332d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824899"
---
# <a name="create-a-hardware-notification-client-driver"></a>创建硬件通知客户端驱动程序


本部分提供了有关如何开发使用 Microsoft 提供的 KMDF 类扩展的硬件通知客户端驱动程序的一般指南。

1.  为客户端驱动程序实现创建一个链接到 Mshwnclxstub 的文件，其中包含标头 hwn 和 hwnclx。

2.  定义所需的 KMDF 和硬件通知类扩展回调函数的实例。 具体而言，必须实现并注册这些回调函数，如下面的示例代码所示。

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

3.  实现[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程，该例程是客户端驱动程序入口点，负责初始化。 对于硬件通知客户端驱动程序，此函数应处理以下内容：

    -   调用[**WDF\_驱动程序\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdf_driver_config_init)初始化驱动程序的[**WDF\_驱动程序\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构。

    -   调用[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)为客户端驱动程序创建框架驱动程序对象。

    -   定义[**HWN\_客户端\_注册\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/ns-hwnclx-_hwn_client_registration_packet)的内容，包括用于类扩展的回调函数指针。 有关所需回调函数的详细信息，请参阅[硬件通知参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

    -   调用[HwNRegisterClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnregisterclient)将客户端驱动程序注册到类扩展。

4.  实现在 PnP 管理器报告设备存在时执行设备初始化操作的[ *\_驱动程序\_设备\_"添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)函数" 的 "\_WDF"。 对于硬件通知客户端驱动程序，此函数应处理以下内容：

    -   调用[**HwNProcessAddDevicePreDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnprocessadddevicepredevicecreate)，它提供 KMDF 将设备转换为不同状态时所需的设备准备/释放和进入/退出回调。

    -   调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)以创建框架设备对象。

    -   调用[**HwNProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnprocessadddevicepostdevicecreate)创建 i/o 队列。

5.  实现定义的[**HWN\_客户端\_初始化\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_initialize_device)函数，该类扩展调用该函数来准备要使用的硬件通知控制器。

6.  实现定义的[**HWN\_客户端\_取消初始化\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_uninitialize_device)函数，该类扩展调用此函数以取消初始化硬件通知控制器。

7.  实现定义的[**HWN\_客户端\_查询\_设备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_query_device_information)函数，该类扩展调用此功能。 此函数负责检索硬件通知组件的属性。

8.  实现定义的[**HWN\_客户端\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_start_device)函数，该类扩展调用此类函数。 此函数负责启动硬件通知控制器并为客户端驱动程序分配 ACPI 资源。

9.  实现定义的[**HWN\_客户端\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_stop_device)函数，该类扩展调用此类函数。 此函数负责停止硬件通知控制器，以及释放客户端驱动程序使用的 ACPI 资源。

10. 实现定义的[**HWN\_客户端\_集\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_set_state)，该状态由类扩展调用。 此函数负责设置硬件通知组件状态。

11. 实现定义的[**HWN\_客户端\_获取\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_get_state)，该状态由类扩展调用。 此函数负责获取硬件通知组件的当前值。 如果输入缓冲区为 NULL，表示用户未指定特定的硬件通知状态，则此函数应返回所有硬件通知组件的状态信息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[硬件通知](hardware-notifications-support.md)

[硬件通知参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)



