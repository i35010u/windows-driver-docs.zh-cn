---
title: 将 NDIS 微型端口驱动程序移植到 NetAdapterCx
description: 将 NDIS 微型端口驱动程序移植到 NetAdapterCx
ms.assetid: F5C798C6-B746-43CB-BF63-DBA7DD0975ED
keywords:
- 将微型端口驱动程序移植到网络适配器类扩展，并将其移植到网络适配器 WDF 类扩展，将 NDIS 1.x 移植到 NetAdapterCx
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2d0d800e5ab51fe0de76f7b077a3bd7de4dcca9c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209007"
---
# <a name="porting-ndis-miniport-drivers-to-netadaptercx"></a>将 NDIS 微型端口驱动程序移植到 NetAdapterCx

本页介绍如何将 NDIS 6. x 微型端口驱动程序转换为 NetAdapterCx 客户端驱动程序。

有关 WDF 的一般信息，请查看[Wdf 驱动程序开发指南](../wdf/index.md)。

## <a name="compilation-settings"></a>编译设置

在 Visual Studio 中打开现有的 NDIS 微型端口驱动程序项目，并使用以下步骤将其转换为 KMDF 项目。

1. 首先，导航到 "**配置属性-> 驱动程序设置-> 驱动程序模型**"，并验证 "**驱动程序类型**" 是否设置为 "KMDF"，并且 " **KMDF 版本**" 和 " **KMDF" 版本**都为空。
2. 在项目属性中，打开 "**驱动程序设置-> 网络适配器驱动程序**"，并将**网络适配器类扩展的链接**设置为 **"是"**。
   * 如果转换后的驱动程序仍将调用 NDIS Api，请继续链接 `ndis.lib`。
3. 删除 NDIS 预处理器宏，如 `NDIS650_MINIPORT=1`。
4. 将以下标头添加到每个源文件（或添加到公共/预编译头）：
  
   ```C++
   #include <ntddk.h>
   #include <wdf.h>
   #include <netadaptercx.h>
   ```
  
5. 将[标准 WDF 修饰](../wdf/specifying-wdf-directives-in-inf-files.md)添加到 INF：
  
   ```INF
   [Yourdriver.Wdf]
   KmdfService = Yourdriverservice, Yourdriver.wdfsect

   [Yourdriver.wdfsect]
   KmdfLibraryVersion = <insert here>
   ```
6. 将新的所需的网络关键字添加到 INF 的 NT 部分：

   - **\*IfConnectorPresent**
   - **\*ConnectionType**
   - **\*DirectionType**
   - **\*AccessType**
   - **\*HardwareLoopback**

     有关这些关键字和示例的详细信息，请参阅[NetAdapterCx 客户端驱动程序的 INF 文件](inf-files-for-netadaptercx-client-drivers.md)。

## <a name="driver-initialization"></a>驱动程序初始化

从[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)中删除对[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的调用，并添加以下内容：

```C++
WDF_DRIVER_CONFIG_INIT(&config, EvtDriverDeviceAdd);
status = WdfDriverCreate(. . . );
if (!NT_SUCCESS(status)) {
  return status;
}
```

如果已设置，则从对[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)的调用中删除**WdfDriverInitNoDispatchOverride**标志。

*DriverUnload*是 WDF 网络客户端驱动程序的可选例程，因此可以根据需要将其删除。 不要从*DriverUnload*调用[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 。

## <a name="device-initialization"></a>设备初始化

接下来，你要将*MiniportInitializeEx*中的代码分发到适当的 WDF 事件回调处理程序中，其中几个是可选的。 有关回调序列的详细信息，请参阅[网络适配器 WDF 客户端驱动程序的启动顺序](power-up-sequence-for-a-netadaptercx-client-driver.md)。

当你启动网络适配器时，但在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前，你将调用等效于[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的方法。 但是，客户端驱动程序将调用不同的功能来设置不同类型的功能，而不是使用泛型[**NDIS_MINIPORT_ADAPTER_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)结构调用一个例程。

有关回调的信息，需要提供和何时启动网络适配器，请参阅[设备和适配器初始化](device-and-adapter-initialization.md)。

## <a name="creating-queues-to-manage-control-requests"></a>创建队列以管理控制请求

接下来，仍在[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)中，设置对象标识符（OID）路径。 OID 路径与 WDF 队列类似，但会获得 Oid 而不是 WDFREQUESTs。

在迁移此时，可以执行两种高级方法。 第一种方法是注册[*EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default)处理程序，该处理程序接收 OID 请求的方式非常类似于微型端口驱动程序从 NDIS 接收请求的方式。 这是最简单的端口，因为您可能只需要从旧的 MINIPORT_OID_REQUEST 处理程序调整函数签名。

另一种方法是拆分 OID 处理程序的 switch 语句，并为每个单独的 OID 提供单独的处理程序。 如果设备需要特定于 OID 的功能，则可以选择此选项。

如果在[**NDIS 6.1 中使用了直接 OID 请求接口**](../network/direct-oid-request-interface-in-ndis-6-1.md)，请将其替换为并行 WDF 队列。 同样，NDIS 中的常规（串行）请求接口应成为顺序的 WDF 队列。

有关为 Oid 注册处理程序的信息，请参阅[处理控制请求](handling-control-requests.md)。

## <a name="reading-configuration-from-the-registry"></a>正在从注册表读取配置

接下来，将对[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)和相关函数的调用替换为 `NetConfiguration*` 方法。 `NetConfiguration*` 方法与 `Ndis*Configuration*` 函数相似，无需重构代码。

有关详细信息，请参阅[访问配置信息](accessing-configuration-information.md)。

## <a name="receiving-io-control-codes-iotcls-from-user-mode"></a>从用户模式接收 i/o 控制代码（IOTCLs）

如果 NDIS 驱动程序调用[**NdisRegisterDeviceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterdeviceex)（用于创建控制设备对象（CDO）以从用户模式接收 IOCTLs），请阅读本部分。

下面是在 WDF 网络客户端驱动程序中执行此操作的两种方法。

最简单的方法是通过从客户端的[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调调用[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)来创建控制设备对象。 有关详细信息，请参阅[使用控制设备对象](../wdf/using-control-device-objects.md)。

但是，建议的解决方法是创建设备接口，如[使用设备接口](using-device-interfaces.md)中所述。

## <a name="finishing-device-initialization"></a>完成设备初始化

在[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)中，你可以执行任何其他操作，例如分配中断。

## <a name="handling-power-state-change-notifications"></a>处理电源状态更改通知

WDF 客户端驱动程序不会收到电源状态更改的[**OID_PNP_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) 。

而 WDF 客户端将注册可选的回调函数以接收电源状态更改通知。 有关概述，请参阅[支持功能驱动程序中的 PnP 和电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)。

通常， [**OID_PNP_SET_POWER**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)处理程序中的代码会移动到[*EVT_WDF_DEVICE_D0_EXIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)并[*EVT_WDF_DEVICE_D0_ENTRY*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)。

由于 WDF 电源状态计算机略有不同，因此你可能需要对代码进行细微的修改。

具体而言，在其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)回调函数中，NDIS 微型端口驱动程序执行一次性初始化任务，并执行工作以使设备进入 D0 状态。 然后，它重复工作以在其[*OID_PNP_SET_POWER*](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)处理程序中转向 D0。

与此相反，WDF 客户端会在[**EVT_WDF_DEVICE_D0_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)之前在事件回调中执行一次性初始化任务，在这种情况下，设备处于低功耗状态。 然后，它会执行[**EVT_WDF_DEVICE_D0_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)中的 D0 操作。

总之，在 WDF 中，将 "转到 D0" 代码放在一个位置，而不是两个位置。

有关回调序列的详细信息，请参阅[NetAdapterCx 客户端驱动程序的启动顺序](power-up-sequence-for-a-netadaptercx-client-driver.md)。

## <a name="querying-and-setting-power-management-capabilities"></a>查询和设置电源管理功能

同样，WDF 客户端驱动程序不会接收[**OID_PM_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)来查询或设置网络适配器的电源管理硬件功能。

相反，驱动程序从 NETPOWERSETTINGS 对象查询必需的 LAN 唤醒（WoL）配置。 有关详细信息，请参阅[配置电源管理](configuring-power-management.md)。

返回的实际标志与对 NDIS 6 微型端口的语义相同，因此不需要对逻辑进行深层更改。 主要区别在于，你现在可以在关机序列中查询这些标志。 请参阅[NetAdapterCx 客户端驱动程序的关闭顺序](power-down-sequence-for-a-netadaptercx-client-driver.md)。

移动此代码后，可以删除[*OID_PNP_SET_POWER*](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)和[*OID_PM_PARAMETERS*](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)的 OID 处理程序。

由于 Get-netadapter 框架使你的设备处于 D0 状态，而主机使用网络接口，因此，客户端通常不实现电源逻辑;默认的 Get-netadapter 电源行为已经足够。

## <a name="data-path"></a>数据路径

数据路径编程模型发生了重大更改。 下面是一些重要的区别：

* 在 Get-netadapter 模型中，网络流量不再每个适配器，如 NDIS 中的，而是每个 WDF 队列。 请参阅[创建 I/o 队列](../wdf/creating-i-o-queues.md)。
* NetAdapterCx 会引入一个由网络数据包组成的环形缓冲区，而不是 NET_BUFFER_LIST 和 NET_BUFFER 池，如下所示：
  * [**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)类似于 NET_BUFFER_LIST + NET_BUFFER。
  * [**NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)与内存描述符列表（MDL）类似。 每个[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)都有一个或多个。
  * 有关替换结构以及如何使用它们的详细信息，请参阅[数据包描述符和扩展](packet-descriptors-and-extensions.md)。
* 在 NDIS 1.x 中，微型端口需要处理开始和暂停语义。 在 NetAdapterCx 模型中，这种情况并不是这样。
* [*EVT_RXQUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nc-netrxqueue-evt_rxqueue_advance)回调类似于 NDIS 1.x 中[**MINIPORT_RETURN_NET_BUFFER_LISTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) 。
* [*EVT_TXQUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nc-nettxqueue-evt_txqueue_advance)回调类似于 NDIS 1.x 中[**MINIPORT_SEND_NET_BUFFER_LISTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 。

## <a name="device-removal"></a>设备删除

WDF NIC 驱动程序的设备删除与任何其他 WDF 设备驱动程序中的相同，无需进行网络特定的处理。 网络数据路径首先关闭，然后是 WDF 设备。 有关 WDF 关闭的信息，请参阅[断开 a 设备的用户](../wdf/a-user-unplugs-a-device.md)。

你的*MiniportHaltEx*处理程序可能分布[*EVT_WDF_DEVICE_D0_EXIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)和[*EVT_WDF_DEVICE_RELEASE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)之间。

WDF 客户端无需删除它创建的 Get-netadapter 或任何 OID 和数据路径队列。 WDF 会自动删除这些对象。

可以删除*MiniportShutdownEx*、 *MiniportResetEx*和*MiniportCheckForHangEx*。 不再支持这些回调。

## <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 函数等效项

大多数 `NdisXxx` 函数可以替换为 WDF 等效项。 通常，您应该会发现您需要从 `NDIS.SYS`导入的功能非常少。

有关函数等效项的列表，请参阅[NDIS-WDF 函数等效项](ndis-wdf-function-equivalents.md)。

## <a name="debugging"></a>调试

请参阅[调试 NetAdapterCx 客户端驱动程序](debugging-a-netadaptercx-client-driver.md)。

[！ Ndiskd get-netadapter](../debugger/-ndiskd-netadapter.md)调试程序扩展显示了与 NDIS 6 驱动程序的结果类似的**结果。**

## <a name="conclusion"></a>总结

使用本主题中的步骤，应该有一个可启动和停止设备的工作驱动程序。
