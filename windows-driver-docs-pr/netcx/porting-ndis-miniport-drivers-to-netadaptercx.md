---
title: 将 NDIS 微型端口驱动程序移植到 NetAdapterCx
description: 将 NDIS 微型端口驱动程序移植到 NetAdapterCx
ms.assetid: F5C798C6-B746-43CB-BF63-DBA7DD0975ED
keywords:
- 将网络适配器类扩展，移植到网络适配器 WDF 类扩展，NDIS 移植到微型端口驱动程序移植到 NetAdapterCx 6.x
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b911cd1a888166419f113e34b09a7dd2da988c13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375339"
---
# <a name="porting-ndis-miniport-drivers-to-netadaptercx"></a>将 NDIS 微型端口驱动程序移植到 NetAdapterCx

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

此页介绍了如何将 NDIS 6.x 微型端口驱动程序转换成 NetAdapterCx 客户端驱动程序。

有关 WDF 的常规信息，请查看[WDF 驱动程序开发指南](../wdf/index.md)。

## <a name="compilation-settings"></a>编译设置

在 Visual Studio 中打开现有 NDIS 微型端口驱动程序项目，并使用以下步骤将其转换为 KMDF 项目。

1. 首先，导航到**配置属性-> 驱动程序设置-> 驱动程序模型**并确认**类型的驱动程序**设为 KMDF，并且**KMDF 主要版本**和**KMDF 版本次要**都为空。
2. 在项目属性中，打开**驱动程序设置-> 网络适配器驱动程序**并设置**链接至网络适配器类扩展**到**是**。
   * 如果您已转换的驱动程序仍将调用 NDIS Api，继续针对链接`ndis.lib`。
3. 删除 NDIS 预处理器宏，如`NDIS650_MINIPORT=1`。
4. 将以下标头添加到每个源文件 （或你常见/预编译标头）：
  
   ```C++
   #include <ntddk.h>
   #include <wdf.h>
   #include <netadaptercx.h>
   ```
  
5. 添加[标准 WDF 修饰](../wdf/specifying-wdf-directives-in-inf-files.md)你 INF 到：
  
   ```INF
   [Yourdriver.Wdf]
   KmdfService = Yourdriverservice, Yourdriver.wdfsect

   [Yourdriver.wdfsect]
   KmdfLibraryVersion = <insert here>
   ```
6. 将新的所需网络关键字添加到你 INF 的 NT 部分：

   - **\*IfConnectorPresent**
   - **\*ConnectionType**
   - **\*DirectionType**
   - **\*AccessType**
   - **\*HardwareLoopback**

     有关这些关键字和示例的详细信息，请参阅[NetAdapterCx 客户端驱动程序的 INF 文件](inf-files-for-netadaptercx-client-drivers.md)。

## <a name="driver-initialization"></a>驱动程序初始化

删除对调用[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)从[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff540807)，并添加以下：

```C++
WDF_DRIVER_CONFIG_INIT(&config, EvtDriverDeviceAdd);
status = WdfDriverCreate(. . . );
if (!NT_SUCCESS(status)) {
  return status;
}
```

如果设置，删除**WdfDriverInitNoDispatchOverride**调用标志[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)。

*DriverUnload*是可选的例程 WDF 网络客户端驱动程序，以便根据需要删除它。 不要调用[ **NdisMDeregisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563578)从*DriverUnload*。

## <a name="device-initialization"></a>设备初始化

接下来，你将分发中的代码*MiniportInitializeEx*到相应 WDF 事件回调处理程序，其中有多个是可选的。 回调序列的详细信息，请参阅[网络适配器 WDF 客户端驱动程序的增益道具序列](power-up-sequence-for-a-netadaptercx-client-driver.md)。

您将调用方法等效于[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)当你准备在启动您的网络适配器，但之前调用[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). 但是，而不是调用具有泛型一个例程[ **NDIS_MINIPORT_ADAPTER_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff565920)结构，客户端驱动程序调用其他函数来设置不同类型的功能。

将需要提供的回调以及何时启动网络适配器的信息，请参阅[设备和适配器初始化](device-and-adapter-initialization.md)。

## <a name="creating-queues-to-manage-control-requests"></a>创建队列管理控制请求

接下来，在上仍[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://msdn.microsoft.com/library/windows/hardware/ff541693)，设置对象标识符 (OID) 路径。 OID 路径建模等 WDF 队列，但你将获得而不是 WDFREQUESTs Oid。

有两种可能需要移植这时的高级别方法。 第一个选项是注册[ *EVT_NET_REQUEST_DEFAULT* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default)接收 OID 的处理程序中非常类似于微型端口驱动程序如何从 NDIS 接收请求的请求。 这是最简单的端口，因为您可能只需要进行调整的函数签名从旧的 MINIPORT_OID_REQUEST 处理程序。

另一个选项是拆分 OID 处理程序的 switch 语句并为每个单个 OID 提供单独的处理程序。 如果你的设备需要 OID 特有的功能，可以选择此选项。

如果您使用了[ **Direct OID 请求接口在 NDIS 6.1**](../network/direct-oid-request-interface-in-ndis-6-1.md)，将其替换为并行 WDF 队列。 同样，NDIS 中的正则 （串行） 请求接口应成为顺序 WDF 队列。

有关 Oid 注册处理程序的信息，请参见[处理控制请求](handling-control-requests.md)。

## <a name="reading-configuration-from-the-registry"></a>从注册表读取配置

接下来，将调用[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)和相关函数使用`NetConfiguration*`方法。 `NetConfiguration*`方法都是类似于`Ndis*Configuration*`函数，并且不需要重构你的代码。

有关详细信息，请参阅[访问配置信息](accessing-configuration-information.md)。

## <a name="receiving-io-control-codes-iotcls-from-user-mode"></a>从用户模式下接收 I/O 控制代码 (IOTCLs)

阅读此部分，如果您的 NDIS 驱动程序调用[ **NdisRegisterDeviceEx**](https://msdn.microsoft.com/library/windows/hardware/ff564518)，用于创建控件设备对象 (CDO) 从用户模式下接收 Ioctl 的例程。

以下是两个方法 WDF 网络客户端驱动程序中执行此操作。

最简单的端口是创建控件设备对象通过调用[ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)从客户端[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调。 有关详细信息，请参阅[使用控制设备对象](../wdf/using-control-device-objects.md)。

但是，建议的解决方案是创建一个在设备接口，如中所述[使用设备接口](using-device-interfaces.md)。

## <a name="finishing-device-initialization"></a>完成设备初始化

在这一时刻[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://msdn.microsoft.com/library/windows/hardware/ff541693)，可以执行你想要初始化你的设备，如分配中断任何其他操作。

## <a name="handling-power-state-change-notifications"></a>处理电源状态更改通知

WDF 客户端驱动程序不会收到[ **OID_PNP_SET_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff569780)的电源状态更改。

相反，WDF 客户端会注册以接收电源状态更改通知的可选的回调函数。 有关概述，请参阅[支持即插即用和功能的驱动程序中的电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)。

通常情况下中的代码您[ **OID_PNP_SET_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff569780)处理程序将移到[ *EVT_WDF_DEVICE_D0_EXIT* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)和[ *EVT_WDF_DEVICE_D0_ENTRY*](https://msdn.microsoft.com/library/windows/hardware/ff540848)。

由于 WDF 电源状态机是略有不同，可能需要稍作修改的代码。

具体来说，在其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)回调函数，NDIS 微型端口驱动程序执行一次性初始化任务，以及工作以使设备保持 D0 状态。 然后，重复的工作以转到 D0 中其[ *OID_PNP_SET_POWER* ](https://msdn.microsoft.com/library/windows/hardware/ff569780)处理程序。

与此相反，WDF 客户端将在事件回调之前执行一次性初始化任务[ **EVT_WDF_DEVICE_D0_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff540848)，期间该设备是包含在低功耗状态。 然后执行工作以转到在 D0 [ **EVT_WDF_DEVICE_D0_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff540848)。

总而言之，WDF，您将"转到 D0"代码放在一个位置，而不是两个。

回调序列的详细信息，请参阅[NetAdapterCx 客户端驱动程序的增益道具序列](power-up-sequence-for-a-netadaptercx-client-driver.md)。

## <a name="querying-and-setting-power-management-capabilities"></a>查询和设置电源管理功能

同样，WDF 客户端驱动程序不会收到[ **OID_PM_PARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff569768)查询或设置电源管理硬件功能的网络适配器。

相反，驱动程序将查询从 NETPOWERSETTINGS 对象所需的 LAN 唤醒 (WoL) 配置。 有关详细信息，请参阅[配置电源管理](configuring-power-management.md)。

您会得到的实际标志具有相同的语义与它们针对 NDIS 6 微型端口，因此无需对逻辑进行深入的更改。 主要区别是，现在可以查询这些标志在电源关闭序列期间。 请参阅[NetAdapterCx 客户端驱动程序的关闭序列](power-down-sequence-for-a-netadaptercx-client-driver.md)。

一旦已移动围绕此代码，可以删除的处理程序中 OID [ *OID_PNP_SET_POWER* ](https://msdn.microsoft.com/library/windows/hardware/ff569780)并[ *OID_PM_PARAMETERS*](https://msdn.microsoft.com/library/windows/hardware/ff569768)。

因为 NetAdapter 框架在 D0 保持你的设备，而主机使用的网络接口，客户端通常不实现 power 逻辑;默认 NetAdapter power 行为就足够了。

## <a name="data-path"></a>数据路径

数据路径编程模型已显著更改。 下面是一些重要差异：

* 在 NetAdapter 模型中，网络流量是不能再每个适配器，如下所示 NDIS，但每个 WDF 队列而不是。 请参阅[创建的 I/O 队列](../wdf/creating-i-o-queues.md)。
* 而不是 NET_BUFFER_LIST 和 NET_BUFFER 池 NetAdapterCx 引入了环形缓冲区组成的网络数据包，而这将映射到 NDIS，如下所示：
  * 一个[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)类似于 NET_BUFFER_LIST + NET_BUFFER。
  * 一个[ **NET_PACKET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)类似于内存描述符列表 (MDL)。 每个[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)具有一个或多个。
  * 替换结构以及如何使用它们的详细信息，请参阅[数据包描述符和扩展](packet-descriptors-and-extensions.md)。
* 在 NDIS 6.x，微型端口需要处理启动和暂停语义。 在 NetAdapterCx 模型中，这不再是这种情况。
* [ *EVT_RXQUEUE_ADVANCE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nc-netrxqueue-evt_rxqueue_advance)回调是类似于[ **MINIPORT_RETURN_NET_BUFFER_LISTS** ](https://msdn.microsoft.com/library/windows/hardware/ff559437)在 NDIS 6.x。
* [ *EVT_TXQUEUE_ADVANCE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nc-nettxqueue-evt_txqueue_advance)回调是类似于[ **MINIPORT_SEND_NET_BUFFER_LISTS** ](https://msdn.microsoft.com/library/windows/hardware/ff559440)在 NDIS 6.x。

## <a name="device-removal"></a>删除设备

WDF NIC 驱动程序的设备删除是与任何其他 WDF 设备驱动程序，与所需的任何网络的特定处理中的相同。 网络数据路径会关闭第一次后, 跟 WDF 设备。 WDF 关闭的信息，请参阅[用户断开设备](../wdf/a-user-unplugs-a-device.md)。

你*MiniportHaltEx*处理程序可能将分布[ *EVT_WDF_DEVICE_D0_EXIT* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)并[ *EVT_WDF_DEVICE_RELEASE_硬件*](https://msdn.microsoft.com/library/windows/hardware/ff540890)。

WDF 客户端不需要删除 NetAdapter 或任何其创建的 OID 和数据路径队列。 WDF 将自动删除这些对象。

可以删除*MiniportShutdownEx*， *MiniportResetEx*并*MiniportCheckForHangEx*。 不再支持这些回调。

## <a name="ndis-wdf-function-equivalents"></a>NDIS-WDF 函数等效项

大多数`NdisXxx`函数可以被替换为 WDF 等效项。 一般情况下，您应发现您需要将从导入的很少功能`NDIS.SYS`。

函数等效项的列表，请参阅[NDIS WDF 函数等效项](ndis-wdf-function-equivalents.md)。

## <a name="debugging"></a>调试

请参阅[调试 NetAdapterCx 客户端驱动程序](debugging-a-netadaptercx-client-driver.md)。

[！ Ndiskd.netadapter](../debugger/-ndiskd-netadapter.md)调试器扩展会显示类似的结果到什么 **！ ndiskd.miniport** NDIS 6 驱动程序的显示。

## <a name="conclusion"></a>结束语

使用本主题中的步骤，应具有有效的驱动程序的启动和停止你的设备。
