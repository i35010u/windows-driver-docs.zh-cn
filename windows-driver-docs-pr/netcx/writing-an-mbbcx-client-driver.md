---
title: 编写 MBB NetAdapterCx 客户端驱动程序
description: 描述 MBB NetAdapter 类扩展和客户端驱动程序必须为 MBB moderm 执行的任务的行为。
ms.assetid: FE69E832-848F-475A-9BF1-BBB198D08A86
keywords:
- 移动宽带 (MBB) WDF 类扩展，MBBCx，移动宽带 NetAdapterCx
ms.date: 03/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18fdbe9f8861a0db9217fdbf4c6276003547a815
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136124"
---
# <a name="writing-an-mbbcx-client-driver"></a>编写 MBBCx 客户端驱动程序

[!include[MBBCx Beta Prerelease](../mbbcx-beta-prerelease.md)]

>[!WARNING]
>本主题中的序列图是仅用于说明目的。 它们不是公共协定，将来可能会有所变动。

## <a name="inf-files-for-mbbcx-client-drivers"></a>MBBCx 客户端驱动程序的 INF 文件

与其他 NetAdapterCx 客户端驱动程序相同的 MBBCx 客户端驱动程序的 INF 文件。 有关详细信息，请参阅[NetAdapterCx 客户端驱动程序的 INF 文件](inf-files-for-netadaptercx-client-drivers.md)。

## <a name="initialize-the-device"></a>初始化设备

除了这些任务所需的有关 NetAdapterCx [NetAdapter 设备初始化](device-and-adapter-initialization.md)，MBB 客户端驱动程序还必须执行以下任务在其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数：

1. 调用[ **MbbDeviceInitConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdeviceinitconfig)后调用[ *NetAdapterDeviceInitConfig* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)但在通过调用[ *WdfDeviceCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)，引用相同[ **WDFDEVICE\_INIT** ](../wdf/wdfdevice_init.md)由框架传入的对象。

2. 调用[ **MbbDeviceInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdeviceinitialize)注册 MBB 特定于设备的回调函数使用一个已初始化[ **MBB_DEVICE_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/ns-mbbcx-_mbb_device_config)从结构和 WDFDEVICE 对象获取*WdfDeviceCreate*。

下面的示例演示如何初始化 MBB 设备。 为清楚起见，错误处理已被省略。

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

与其他类型的 NetAdapterCx 驱动程序，不同 MBB 客户端驱动程序必须创建 NETADAPTER 对象内*EvtDriverDeviceAdd*回调函数。 相反，它会指示 MBBCx 由为此，更高版本。

接下来，客户端驱动程序必须调用[ **MbbDeviceSetMbimParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdevicesetmbimparameters)，通常在[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调下面的函数。

此消息流关系图说明了初始化过程。

![MBBCx 客户端驱动程序初始化过程](images/mbbcx_initializing.png)

此消息流关系图说明了初始化过程。

![MBBCx 客户端驱动程序初始化过程](images/mbbcx_initializing.png)

## <a name="handling-mbim-control-messages"></a>处理 MBIM 控制消息

MBBCx 使用 MBIM 规范 1.0，部分 8、 9 和 10，控制平面中定义的标准 MBIM 控制命令。 命令和响应通过一系列客户端驱动程序提供的回调函数和提供的 MBBCx Api 进行交换。 通过使用这些函数调用 MBIM 规范 1.0，5.3、 部分中定义，MBBCx 模仿 MBIM 设备的操作模式：

- MBBCx 将 MBIM 命令消息发送到客户端驱动程序，通过调用其[ *EvtMbbDeviceSendMbimFragment* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/nc-mbbcx-evt_mbb_device_send_mbim_fragment)回调函数。 客户端驱动程序将通过调用以异步方式完成此发送请求[ **MbbRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbrequestcomplete)。
- 客户端驱动程序通过调用表示结果的可用性[ **MbbDeviceResponseAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdeviceresponseavailable)。
- MBBCx 中提取 MBIM 响应消息从客户端驱动程序通过调用其[ *EvtMbbDeviceReceiveMbimFragment* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_receive_mbim_fragment)回调函数。 客户端驱动程序将通过调用以异步方式完成此获取响应请求[ **MbbRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbrequestcompletewithinformation)。
- MBB 客户端驱动程序可以通过调用通知的未经请求的设备事件 MBBCx **MbbDeviceResponseAvailable**。 MBBCx 然后检索的信息从客户端驱动程序同样到它如何提取 MBIM 响应消息。

下图说明了 MBBCx 客户端驱动程序消息交换流。

![Mbim 消息交换](images/mbim.png)

### <a name="synchronization-of-mbim-control-messages"></a>MBIM 控制消息的同步

MBBCx framework 总是序列化到客户端驱动程序调用*EvtMbbDeviceSendMbimFragment*并*EvtMbbDeviceReceiveMbimFragment*回调函数。 直到客户端驱动程序调用任何一个，将由框架所做的任何新的调用**MbbRequestComplete**或**MbbRequestCompleteWithInformation**。

虽然客户端驱动程序保证不会接收重叠*EvtMbbDeviceSendMbimFragment*或*EvtMbbDeviceReceiveMbimFragment*回调，它可能会收到多个调用连续前一命令的响应才可从该设备。

如果设备处于*D0*状态，则 MBBCx framework 首次将设备添加到 D0 (换而言之，它将调用[ *EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)) 调用之前*EvtMbbDeviceSendMbimFragment*或*EvtMbbDeviceReceiveMbimFragment*。 MBBCx 框架还可确保，它将保留在设备处于 D0 状态，这意味着它将不会调用[ *EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)，直到客户端调用**MbbRequestComplete**或**MbbRequestCompleteWithInformation**。

## <a name="creating-the-netadapter-interface-for-the-pdp-contexteps-bearer"></a>为 PDP 上下文/EPS 持有者创建的 NetAdapter 接口

之前建立的数据的会话，MBBCx 将指示客户端驱动程序，以创建 NETADAPTER 对象，它将由 MBBCx 来激活数据会话表示网络接口。 这通过 MBBCx 调入客户端驱动程序的实现[ *EvtMbbDeviceCreateAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter)回调函数。

在实现中的*EvtMbbDeviceCreateAdapter*回调函数 MBBCx 客户端驱动程序必须首先执行相同的任务创建任何 NetAdapterCx 客户端驱动程序的 NETADAPTER 对象所需的。 此外，它还必须执行以下额外任务：

1. 调用[ **MbbAdapterInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbadapterinitialize)上创建的 NETADAPTER 对象[ *NetAdapterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)。

2. 在调用*MbbAdapterinitialize*，调用[ **MbbAdapterGetSessionId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbadaptergetsessionid)哪些 MBBCx 数据会话 ID 想要使用此 NETADAPTER 对象的检索。 例如，如果返回的值为 0，则意味着 MBBCx 数据会话建立主 PDP 上下文/默认 EPS 持有者将使用此 NETADAPTER 接口。

3. 我们建议 MBBCx 客户端驱动程序将创建的 NETADAPTER 对象和返回之间的内部映射*SessionId*。 这有助于跟踪数据会话 NETADAPTER 对象关系，在多个 PDP 上下文/EPS 承载已激活时尤其有用。

4. 返回从之前*EvtMbbDeviceCreateAdapter*，客户端驱动程序必须启动适配器通过调用[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)。 或者，他们还可以通过调用一个或多个这些函数设置适配器的功能*之前*调用**NetAdapterStart**:
    - [**NetAdapterSetDatapathCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)
    - [**NetAdapterSetLinkLayerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetlinklayercapabilities)
    - [**NetAdapterSetLinkLayerMtuSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetlinklayermtusize)
    - [**NetAdapterSetPowerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetpowercapabilities)

MBBCx 至少一次，调用此回调函数，因此始终主 PDP 上下文/默认 EPS 持有者的一个 NETADPATER 对象。 如果激活了多个 PDP 上下文/EPS 承载，MBBCx 可能调用此回调函数多次，一次用于建立每个数据会话。 之间由 NETADAPTER 对象和数据工作期，如以下关系图中所示的网络接口必须是一对一的关系。

![多个 NetAdapters](images/multi-netadapter.png)

下面的示例演示如何为数据会话创建 NETADAPTER 对象。 请注意，错误处理和所需的设置适配器功能的代码省略了简洁和清晰度。

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

设置数据路径功能的代码示例，请参阅[网络数据缓冲区管理](network-data-buffer-management.md)。

它调用 MBBCx 保证*EvtMbbDeviceCreateAdapter*请求之前**MBIM_CID_CONNECT**相同的会话 id。 以下流程图显示了客户端驱动程序和类扩展之间的交互创建 NETADAPTER 对象。  

![NETADAPTER 创建和激活 MBB 客户端驱动程序](images/activation.png)

创建由 MBBCx 启动主 PDP 上下文/默认 EPS 持有者的 NETADAPTER 对象的流时[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)已成功完成。

用于创建 NETADAPTER 对象，通过触发辅助 PDP 上下文/专用 EPS 持有者的流*WwanSvc*按需连接由应用程序的请求时。

### <a name="lifetime-of-the-netadapter-object"></a>NETADAPTER 对象的生存期

不再使用时，将由 MBBCx 自动销毁由客户端驱动程序创建的 NETADAPTER 对象。 例如，发生这种情况后附加 PDP 上下文/EPS 承载处于非活动状态。 **不能调用 MBBCx 客户端驱动程序[WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)他们创建的 NETADAPTER 对象。**

如果客户端驱动程序所需清理上下文数据绑定到 NETADAPTER 对象，它应提供[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)对象中的函数调用时特性结构**NetAdapterCreate**。  

## <a name="power-management-of-the-mbb-device"></a>MBB 设备的电源管理

电源管理的客户端驱动程序应使用 NETPOWERSETTINGS 对象[等其他类型的 NetAdapterCx 客户端驱动程序](configuring-power-management.md)。

## <a name="handling-device-service-sessions"></a>处理设备服务会话

当应用程序发送到调制解调器设备 DSS 数据时，MBBCx 调用客户端驱动程序[ *EvtMbbDeviceSendServiceSessionData* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_send_device_service_session_data)回调函数。 客户端驱动程序应然后异步发送数据到该设备并调用[ **MbbDeviceSendDeviceServiceSessionDataComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdevicesenddeviceservicesessiondatacomplete)完成后发送，因此 MBBCx 然后可以释放的内存分配的数据。

相反，客户端驱动程序调用[ **MbbDeviceReceiveDeviceServiceSessionData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdevicereceivedeviceservicesessiondata)传递由 MBBCx 通过应用程序的任何数据。
