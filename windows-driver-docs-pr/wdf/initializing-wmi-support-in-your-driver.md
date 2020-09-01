---
title: 在驱动程序中初始化 WMI 支持
description: 在驱动程序中初始化 WMI 支持
ms.assetid: cf79176c-8e08-45f9-b2fb-a82707d8667b
keywords:
- WMI WDK KMDF，初始化支持
- 提供程序实例 WDK KMDF
- 多个提供程序实例 WDK KMDF
- 单个提供程序实例 WDK KMDF
- 注册 MOF 资源名称 WDK KMDF
- MOF 资源名称 WDK KMDF
- 初始化 WMI 支持 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8ebb2798f7e7486c6a528e5e1e2596a6b90353b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184163"
---
# <a name="initializing-wmi-support-in-your-driver"></a>在驱动程序中初始化 WMI 支持


\[仅适用于 KMDF\]

若要支持 WMI 数据块，请使用基于框架的驱动程序：

-   将托管对象格式注册 (MOF) 未在 *Wmicore*中定义的任何自定义 WMI 数据提供程序的资源名称。

-   创建一个或多个 WMI 实例对象，以表示它可以读取或写入的数据块。

-   （可选）实现一个或多个事件回调函数以提供驱动程序提供的 WMI 数据。

-   注册每个 WMI 实例对象，使其可供 WMI 客户端使用。

若要初始化其 WMI 支持，KMDF 驱动程序应在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 或 [*EvtDeviceSelfManagedIoInit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init) 回调中执行以下步骤：

1.  提供 MOF 文件以支持自定义 WMI 数据提供程序的驱动程序必须调用 [**WdfDeviceAssignMofResourceName**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignmofresourcename) 方法来注册 MOF 资源名称，然后驱动程序才会创建表示该数据提供程序的 WMI 提供程序对象。

2.  初始化 WMI 提供程序配置结构，并根据需要 (WDFWMIPROVIDER) 创建 WMI 提供程序对象。
3.  初始化 WMI 实例配置结构，并 (WDFWMIINSTANCE) 创建 WMI 实例对象。

默认情况下，当 KMDF 驱动程序创建其第一个 WMI 实例时，框架会创建 WMI 提供程序。 因此，如果驱动程序只需要一个 WMI 提供程序，则不需要 ([**WdfWmiProviderCreate**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiprovidercreate)) 调用提供程序创建方法。 但是，驱动程序必须填写提供程序配置结构，因为此结构提供框架在创建实例时所使用的提供程序的相关信息。

如果你的驱动程序创建它支持的每个 WMI 数据块的单个实例，则驱动程序将调用 [**WdfWmiInstanceCreate**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)，同时同时传递 [**wdf \_ wmi \_ 提供程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_provider_config) 结构和 [**wdf \_ wmi \_ 实例 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config) 结构。 此单个调用将配置单个框架提供的 WMI 提供程序对象，并创建 WMI 实例对象。

如果驱动程序创建其 WMI 数据块的多个实例，则驱动程序必须同时调用 [**WdfWmiProviderCreate**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiprovidercreate) 和 [**WdfWmiInstanceCreate**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)

### <a name="registering-provider-instances"></a><a href="" id="registering-provider-instances"></a> 注册提供程序实例

在 WMI 客户端可以访问驱动程序的 WMI 数据块之前，驱动程序必须向系统的 WMI 服务注册其提供程序实例。 驱动程序可以使用以下任一方法来注册提供程序实例：

-   将提供程序实例的[**WDF \_ WMI \_ 实例 \_ 配置**](/windows-hardware/drivers/ddi/wdfwmi/ns-wdfwmi-_wdf_wmi_instance_config)结构的**Register**成员设置为**TRUE**。

    如果你的驱动程序将 " **注册** " 设置为 " **TRUE**"，则在设备首次进入工作状态 (D0) 状态时，框架会自动注册该实例。

-   调用 [**WdfWmiInstanceRegister**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstanceregister) 方法。

    如果在调用[**WdfWmiInstanceCreate**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)后，你的驱动程序调用[**WdfWmiInstanceRegister**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstanceregister) ，框架将在设备处于工作状态 (D0) 状态后注册该实例。

)  (删除 [*实例的设备*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup) 时，框架会自动注销每个提供程序实例。 有关框架调用驱动程序的回调函数的顺序的信息，请参阅 [PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

你的驱动程序可以通过调用 [**WdfWmiInstanceDeregister**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancederegister)随时取消注册实例。

 

