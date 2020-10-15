---
title: 写入 MBB-NetAdapterCx 客户端驱动程序
description: 描述 MBB-NetAdapter 类扩展和客户端驱动程序必须为 MBB moderm 执行的任务的行为。
ms.assetid: FE69E832-848F-475A-9BF1-BBB198D08A86
keywords:
- Mobile 宽带 (MBB) WDF 类扩展，MBBCx，Mobile 宽带 NetAdapterCx
ms.date: 03/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: c77b47fe0e5fd7458a4a8f150845f6b9b7a31a54
ms.sourcegitcommit: a3ccb07628a9cd8936d7f88f4aab8faf9379cae5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92088121"
---
# <a name="writing-an-mbbcx-client-driver"></a>编写 MBBCx 客户端驱动程序

>[!WARNING]
>本主题中的序列图仅用于说明目的。 它们不是公共协定，将来可能会更改。

## <a name="inf-files-for-mbbcx-client-drivers"></a>MBBCx 客户端驱动程序的 INF 文件

MBBCx 客户端驱动程序的 INF 文件与其他 NetAdapterCx 客户端驱动程序相同。 有关详细信息，请参阅 [NetAdapterCx 客户端驱动程序的 INF 文件](inf-files-for-netadaptercx-client-drivers.md)。

## <a name="initialize-the-device"></a>初始化设备

除了 NetAdapterCx for [get-netadapter 设备初始化](device-and-adapter-initialization.md)所需的那些任务，MBB 客户端驱动程序还必须在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中执行以下任务：

1. 在调用[*NetAdapterDeviceInitConfig*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig)之后但在调用[*WdfDeviceCreate*](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之前调用[**MBB_DEVICE_CONFIG_INIT**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbb_device_config_init) ，并引用框架传入的同一[**WDFDEVICE \_ INIT**](../wdf/wdfdevice_init.md)对象。

2. 调用 [**MbbDeviceInitialize**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdeviceinitialize) ，以使用初始化的 [**MBB_DEVICE_CONFIG**](/windows-hardware/drivers/ddi/mbbcx/ns-mbbcx-_mbb_device_config) 结构和从 *WdfDeviceCreate*获取的 WDFDEVICE 对象来注册 MBB 特定于设备的回调函数。

下面的示例演示如何初始化 MBB 设备。 为清楚起见，已省略错误处理。

```C++
    status = NetAdapterDeviceInitConfig(deviceInit);
    status = MbbDeviceInitConfig(deviceInit);

    // Set up other callbacks such as Pnp and Power policy

    status = WdfDeviceCreate(&deviceInit, &deviceAttributes, &wdfDevice);

    MBB_DEVICE_CONFIG mbbDeviceConfig;
    MBB_DEVICE_CONFIG_INIT(&mbbDeviceConfig,
                           EvtMbbDeviceSendMbimFragment,
                           EvtMbbDeviceReceiveMbimFragment,
                           EvtMbbDeviceSendServiceSessionData,
                           EvtMbbDeviceCreateAdapter);

    status = MbbDeviceInitialize(wdfDevice, &mbbDeviceConfig);
```

与其他类型的 NetAdapterCx 驱动程序不同，MBB 客户端驱动程序不能从 *EvtDriverDeviceAdd* 回调函数中创建 get-netadapter 对象。 相反，它将由 MBBCx 进行指示。

接下来，客户端驱动程序必须调用 [**MbbDeviceSetMbimParameters**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdevicesetmbimparameters)，通常在后面的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数中。

此消息流关系图说明了初始化过程。

![MBBCx 客户端驱动程序初始化过程](images/mbbcx_initializing.png)

此消息流关系图说明了初始化过程。

![MBBCx 客户端驱动程序初始化过程](images/mbbcx_initializing.png)

## <a name="handling-mbim-control-messages"></a>处理 MBIM 控制消息

MBBCx 使用在 MBIM 规范 Rev 1.0 中定义的标准 MBIM 控制命令，第8、9和10部分用于控制平面。 通过一组由 MBBCx 提供的客户端驱动程序和 Api 提供的回调函数来交换命令和响应。 MBBCx 通过使用以下函数调用来模拟 MBIM 设备的操作模型，如 MBIM 规范 Rev 5.3 1.0 中所定义的：

- MBBCx 通过调用其 [*EvtMbbDeviceSendMbimFragment*](/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_send_mbim_fragment) 回调函数向客户端驱动程序发送 MBIM 命令消息。 客户端驱动程序通过调用 [**MbbRequestComplete**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbrequestcomplete)以异步方式完成此发送请求。
- 客户端驱动程序通过调用 [**MbbDeviceResponseAvailable**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdeviceresponseavailable)来通知结果的可用性。
- MBBCx 通过调用其 [*EvtMbbDeviceReceiveMbimFragment*](/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_receive_mbim_fragment) 回调函数从客户端驱动程序中提取 MBIM 响应消息。 客户端驱动程序通过调用 [**MbbRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbrequestcompletewithinformation)以异步方式完成此获取响应请求。
- MBB 客户端驱动程序可能会通过调用 **MbbDeviceResponseAvailable**通知 MBBCx 未经请求的设备事件。 然后，MBBCx 将从客户端驱动程序中检索信息，类似于获取 MBIM 响应消息的方式。

下图说明了 MBBCx-客户端驱动程序消息交换流。

![Mbim 消息交换](images/mbim.png)

### <a name="synchronization-of-mbim-control-messages"></a>同步 MBIM 控制消息

MBBCx 框架始终将调用序列化为客户端驱动程序的 *EvtMbbDeviceSendMbimFragment* 和 *EvtMbbDeviceReceiveMbimFragment* 回调函数。 在客户端驱动程序调用 **MbbRequestComplete** 或 **MbbRequestCompleteWithInformation**之前，框架不会进行任何新的调用。

虽然保证客户端驱动程序不会收到重叠的 *EvtMbbDeviceSendMbimFragment* 或 *EvtMbbDeviceReceiveMbimFragment* 回调，但它可能会在设备上提供上一个命令的响应之前连续收到对它们的多个调用。

如果设备未处于*d0*状态，MBBCx 框架将首先使设备进入 d0 (换言之，它会在调用*EvtMbbDeviceSendMbimFragment*或*EvtMbbDeviceReceiveMbimFragment*之前调用[*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)) 。 MBBCx 框架还保证设备处于 D0 状态，这意味着它将不会调用 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)，直到客户端调用 **MbbRequestComplete** 或 **MbbRequestCompleteWithInformation**。

## <a name="creating-the-netadapter-interface-for-the-pdp-contexteps-bearer"></a>为 PDP 上下文/EPS 持有者创建 Get-netadapter 接口

在建立数据会话之前，MBBCx 将指示客户端驱动程序创建 GET-NETADAPTER 对象，并且 MBBCx 将使用它来表示激活的数据会话的网络接口。 这是通过 MBBCx 调用客户端驱动程序的 [*EvtMbbDeviceCreateAdapter*](/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter) 回调函数实现的。

在 *EvtMbbDeviceCreateAdapter* 回调函数的实现中，MBBCx 客户端驱动程序必须先执行创建 get-netadapter 对象所需的相同任务（作为任何 NetAdapterCx 客户端驱动程序）。 此外，它还必须执行以下附加任务：

1. 对[*NetAdapterCreate*](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)创建的 get-netadapter 对象调用[**MbbAdapterInitialize**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbadapterinitialize) 。

2. 调用 *MbbAdapterinitialize*后，调用 [**MbbAdapterGetSessionId**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbadaptergetsessionid) 来检索 MBBCX 打算使用此 get-netadapter 对象的数据会话 ID。 例如，如果返回值为0，则表示 MBBCx 将使用此 GET-NETADAPTER 接口来表示由主 PDP 上下文/默认 EPS 持有者建立的数据会话。

3. 建议 MBBCx 客户端驱动程序在创建的 GET-NETADAPTER 对象和返回的 *SessionId*之间保留内部映射。 这有助于跟踪数据会话间 GET-NETADAPTER 对象关系，这在激活多个 PDP 上下文/EPS bearers 时特别有用。

4. 从 *EvtMbbDeviceCreateAdapter*返回之前，客户端驱动程序必须通过调用 [**NetAdapterStart**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)来启动适配器。 此外，还可以在调用**NetAdapterStart***之前*调用一个或多个此类函数来设置适配器的功能：
    - [**NetAdapterSetDatapathCapabilities**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)
    - [**NetAdapterSetLinkLayerCapabilities**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetlinklayercapabilities)
    - [**NetAdapterSetLinkLayerMtuSize**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetlinklayermtusize)

MBBCx 至少调用此回调函数一次，因此主 PDP 上下文/默认 EPS 持有者始终有一个 NETADPATER 对象。 如果激活了多个 PDP 上下文/EPS bearers，MBBCx 可能会多次调用此回调函数，每个数据会话将被建立。 GET-NETADAPTER 对象和数据会话所表示的网络接口之间必须存在一对一的关系，如下图所示。

![多个 NetAdapters](images/multi-netadapter.png)

下面的示例演示如何为数据会话创建 GET-NETADAPTER 对象。 请注意，为了简洁和清晰起见，设置适配器功能所需的错误处理和代码会保持不变。

```C++
    NTSTATUS
    EvtMbbDeviceCreateAdapter(
        WDFDEVICE  Device,
        PNETADAPTER_INIT AdapterInit
    )
    {
        // Get the client driver defined per-device context
        PMY_DEVICE_CONTEXT deviceContext = MyGetDeviceContext(Device);

        // Set up the client driver defined per-adapter context
        WDF_OBJECT_ATTRIBUTES adapterAttributes;
        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&adapterAttributes,
                                                MY_NETADAPTER_CONTEXT);


        // Create the NETADAPTER object
        NETADAPTER netAdapter;
        NTSTATUS status = NetAdapterCreate(AdapterInit,
                                           &adapterAttributes,
                                           &netAdapter);

        // Initialize the adapter for MBB
        status = MbbAdapterInitialize(netAdapter);

        // Retrieve the Session ID and use an array to store
        // the session <-> NETADAPTER object mapping
        ULONG sessionId;
        PMY_NETADAPTER_CONTEXT netAdapterContext = MyGetNetAdapterContext(netAdapter);

        netAdapterContext->NetAdapter = netAdapter;

        sessionId = MbbAdapterGetSessionId(netAdapter);

        netAdapterContext->SessionId = sessionId;

        deviceContext->Sessions[sessionId].NetAdapterContext = netAdapterContext;

        //
        // Optional: set adapter capabilities
        //
        ...
        NetAdapterSetDatapathCapabilities(netAdapter,
                                          &txCapabilities,
                                          &rxCapabilities);

        ...
        NetAdapterSetLinkLayerCapabilities(netAdapter,
                                           &linkLayerCapabilities);

        ...
        NetAdapterSetLinkLayerMtuSize(netAdapter,
                                      MY_MAX_PACKET_SIZE - ETHERNET_HEADER_LENGTH);

        //
        // Required: start the adapter
        //
        status = NetAdapterStart(netAdapter);

        return status;
    }
```

有关设置数据路径功能的代码示例，请参阅 [网络数据缓冲区管理](network-data-buffer-management.md)。

MBBCx 保证在请求具有相同会话 ID 的**MBIM_CID_CONNECT**之前调用*EvtMbbDeviceCreateAdapter* 。 以下流程图显示了客户端驱动程序和类扩展在创建 GET-NETADAPTER 对象中的交互。  

![GET-NETADAPTER MBB 客户端驱动程序的创建和激活](images/activation.png)

当 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 成功完成后，MBBCx 将启动主 PDP 上下文/默认 EPS 持有者的 get-netadapter 对象创建的流。

当应用程序请求按需连接时， *WwanSvc* 会触发为辅助 PDP 上下文/专用 EPS 持有者创建 get-netadapter 对象的流。

### <a name="lifetime-of-the-netadapter-object"></a>GET-NETADAPTER 对象的生存期

当 MBBCx 不再使用时，由客户端驱动程序创建的 GET-NETADAPTER 对象将自动销毁。 例如，在停用额外的 PDP 上下文/EPS bearers 后，会发生这种情况。 **MBBCx 客户端驱动程序不能在其创建的 GET-NETADAPTER 对象上调用 [WdfObjectDelete](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 。**

如果客户端驱动程序需要清除绑定到 GET-NETADAPTER 对象的上下文数据，则在调用**NetAdapterCreate**时，它应在对象属性结构中提供[*EvtDestroyCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)函数。  

## <a name="power-management-of-the-mbb-device"></a>MBB 设备的电源管理

对于电源管理，客户端驱动程序应使用 [类似于其他类型的 NetAdapterCx 客户端驱动程序](configuring-power-management.md)的 NETPOWERSETTINGS 对象。

## <a name="handling-device-service-sessions"></a>处理设备服务会话

当应用程序将 DSS 数据发送到调制解调器设备时，MBBCx 调用客户端驱动程序的 [*EvtMbbDeviceSendServiceSessionData*](/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_send_device_service_session_data) 回调函数。 然后，客户端驱动程序应将数据异步发送到设备，并在发送完成后调用 [**MbbDeviceSendDeviceServiceSessionDataComplete**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdevicesenddeviceservicesessiondatacomplete) ，以便 MBBCx 可以释放为数据分配的内存。

相反，客户端驱动程序调用 [**MbbDeviceReceiveDeviceServiceSessionData**](/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdevicereceivedeviceservicesessiondata) ，通过 MBBCx 将任何数据传递到应用程序。