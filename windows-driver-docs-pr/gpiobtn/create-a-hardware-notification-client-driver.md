---
title: 创建硬件通知客户端驱动程序
description: 本部分提供了有关如何开发使用 Microsoft 提供的 KMDF 类扩展的硬件通知客户端驱动程序的一般指南。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0d0bdd7ed2f018d3938a729af5847152baac093
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090964"
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

3.  实现 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程，该例程是客户端驱动程序入口点，负责初始化。 对于硬件通知客户端驱动程序，此函数应处理以下内容：

    -   调用 [**WDF \_ 驱动程序 \_ 配置 \_ INIT**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdf_driver_config_init) 初始化驱动程序的 [**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config) 结构。

    -   调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 为客户端驱动程序创建框架驱动程序对象。

    -   定义 [**HWN \_ 客户端 \_ 注册 \_ 包**](/windows-hardware/drivers/ddi/hwnclx/ns-hwnclx-_hwn_client_registration_packet)的内容，包括类扩展使用的回调函数指针。 有关所需回调函数的详细信息，请参阅 [硬件通知参考](/windows-hardware/drivers/ddi/index)。

    -   调用 [HwNRegisterClient](/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnregisterclient) 将客户端驱动程序注册到类扩展。

4.  实现一个用于在 PnP 管理器报告设备存在时执行设备初始化操作的 [*.Evt \_ WDF \_ DRIVER \_ DEVICE \_ ADD*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 函数。 对于硬件通知客户端驱动程序，此函数应处理以下内容：

    -   调用 [**HwNProcessAddDevicePreDeviceCreate**](/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnprocessadddevicepredevicecreate)，它提供 KMDF 将设备转换为不同状态时所需的设备准备/释放和进入/退出回调。

    -   调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 以创建框架设备对象。

    -   调用 [**HwNProcessAddDevicePostDeviceCreate**](/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnprocessadddevicepostdevicecreate) 创建 i/o 队列。

5.  实现定义的 [**HWN \_ CLIENT \_ INITIALIZE \_ 设备**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_initialize_device) 函数，该类扩展调用该函数来准备要使用的硬件通知控制器。

6.  实现定义的 [**HWN \_ 客户端 \_ 初始化 \_ 设备**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_uninitialize_device) 函数，该类扩展调用此函数以取消初始化硬件通知控制器。

7.  实现定义的 [**HWN \_ 客户端 \_ 查询 \_ 设备 \_ 信息**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_query_device_information) 函数，该类扩展调用此函数。 此函数负责检索硬件通知组件的属性。

8.  实现定义的 [**HWN \_ 客户端 \_ 启动 \_ 设备**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_start_device) 函数，该类扩展调用此函数。 此函数负责启动硬件通知控制器并为客户端驱动程序分配 ACPI 资源。

9.  实现定义的 [**HWN \_ CLIENT \_ STOP \_ 设备**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_stop_device) 函数，该类扩展调用此函数。 此函数负责停止硬件通知控制器，以及释放客户端驱动程序使用的 ACPI 资源。

10. 实现由类扩展调用的已定义 [**HWN \_ 客户端 \_ 集 \_ 状态**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_set_state)。 此函数负责设置硬件通知组件状态。

11. 实现由类扩展调用的已定义 [**HWN \_ 客户端 \_ 获取 \_ 状态**](/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_get_state)。 此函数负责获取硬件通知组件的当前值。 如果输入缓冲区为 NULL，表示用户未指定特定的硬件通知状态，则此函数应返回所有硬件通知组件的状态信息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[硬件通知](hardware-notifications-support.md)

