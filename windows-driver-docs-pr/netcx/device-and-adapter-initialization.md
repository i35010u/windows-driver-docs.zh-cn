---
title: 设备和适配器初始化
description: 设备和适配器初始化
ms.assetid: EBBEF0FB-6CDB-4899-AAE9-71812EE20AFB
keywords:
- NetAdapterCx 设备初始化、 NetCx 设备初始化、 NetAdapterCx 适配器初始化、 NetCx 适配器初始化
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fbd4bfca2a0026f133e1b7b445f56a42c147e3b3
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903747"
---
# <a name="device-and-adapter-initialization"></a>设备和适配器初始化

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

本主题介绍 NetAdapterCx 客户端驱动程序来初始化并启动 WDFDEVICE 和 NETADAPTER 对象的步骤。 有关这些对象和其关系的详细信息，请参阅[NetAdapterCx 摘要对象](summary-of-netadaptercx-objects.md)。

## <a name="evtwdfdriverdeviceadd"></a>EVT_WDF_DRIVER_DEVICE_ADD

NetAdapterCx 客户端驱动程序注册其[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)时，它调用的回调函数[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)从其[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff540807)例程。

在中[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)，NetAdapterCx 客户端驱动程序应执行以下操作顺序：

1. 调用[ **NetAdapterDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)。

    ```C++
    status = NetAdapterDeviceInitConfig(DeviceInit);
    if (!NT_SUCCESS(status)) 
    {
        return status;
    }
    ```

2. 调用[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。 

    > [!TIP]
    > 如果设备支持多个 NETADAPTER，我们建议在设备上下文中存储指向每个适配器。

3. 创建 NETADAPTER 对象。 若要执行此操作，客户端调用[ **NetAdapterInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterinitallocate)后, 跟可选**NetAdapterInitSetXxx**方法添加到 initailize 适配器的特性。 最后，客户端调用[ **NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)。 

    下面的示例演示客户端驱动程序可能会如何初始化 NETADAPTER 对象。 请注意在此示例中简化了错误处理。

    ```C++
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attribs, MY_ADAPTER_CONTEXT);

    //
    // Allocate the initialization structure
    //
    PNETADAPTER_INIT adapterInit = NetAdapterInitAllocate(device);
    if(adapterInit == NULL)
    {
        return status;
    }        

    //
    // Optional: set additional attributes
    //

    // Datapath callbacks for creating packet queues
    PNET_ADAPTER_DATAPATH_CALLBACKS datapathCallbacks;
    NET_ADAPTER_DATAPATH_CALLBACKS_INIT(datapathCallbacks,
                                        MyEvtAdapterCreateTxQueue,
                                        MyEvtAdapterCreateRxQueue);
    NetAdapterInitSetDatapathCallbacks(adapterInit,
                                       datapathCallbacks);

    // Power settings attributes
    NetAdapterInitSetNetPowerSettingsAttributes(adapterInit,
                                                attribs);

    // Net request attributes
    NetAdapterInitSetNetRequestAttributes(adapterInit,
                                            attribs);

    // 
    // Required: create the adapter
    //
    NETADAPTER* netAdapter;
    status = NetAdapterCreate(adapterInit, &attribs, netAdapter);
    if(!NT_SUCCESS(status))
    {
        NetAdapterInitFree(adapterInit);
        adapterInit = NULL;
        return status;
    }

    //
    // Required: free the adapter initialization object even 
    // if adapter creation succeeds
    //
    NetAdapterInitFree(adapterInit);
    adapterInit = NULL;

    //
    // Optional: initialize the adapter's context
    //
    PMY_ADAPTER_CONTEXT adapterContext = GetMyAdapterContext(&netAdapter);
    ...
    ```

（可选） 你可以将上下文空间添加到 NETADAPTER 对象中。 由于可以在任何 WDF 对象上设置上下文，您可以添加单独的上下文空间 WDFDEVICE 和 NETADAPTER 对象。 在步骤 3 中示例中，客户端添加`MY_ADAPTER_CONTEXT`NETADAPTER 对象。 有关详细信息，请参阅[框架对象上下文空间](../wdf/framework-object-context-space.md)。

我们建议你 WDFDEVICE 将与设备相关的数据放在上下文中并与网络相关的数据，如链路层地址到 NETADAPTER 上下文。 如果要将迁移现有的 NDIS 6.x 驱动程序，可能会有将与网络有关和与设备相关数据组合到单个数据结构单一 MiniportAdapterContext。 为了简化迁移过程，只需将该整个结构转换为 WDFDEVICE 上下文，并使一个小结构，其中指向 WDFDEVICE 的上下文的 NETADAPTER 的上下文。

你可以选择提供到 2 个回调[ **NET_ADAPTER_DATAPATH_CALLBACKS_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)方法：

* [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)
* [*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)

有关在要提供的这些回调实现中的详细信息，请参阅各个参考页。

## <a name="evtwdfdevicepreparehardware"></a>EVT_WDF_DEVICE_PREPARE_HARDWARE

许多 NetAdapterCx 客户端驱动程序中启动其适配器及其[ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数，但值得注意的例外[移动宽带类扩展客户端驱动程序](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)。 若要注册*EVT_WDF_DEVICE_PREPARE_HARDWARE* NetAdapterCx 客户端驱动程序必须调用回调函数[ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)。 

在中[ *EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)，除了其他硬件准备任务之外的客户端驱动程序必须调用[ **NetAdapterStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). 这样做之前，驱动程序可以选择性地设置适配器的功能。

下面的示例演示如何客户端驱动程序可能会启动 NETADAPTER 对象。 请注意，所需的设置适配器功能的每个方法的代码为了简单起见和清楚起见，省略了简化的错误处理。

```C++
PMY_DEVICE_CONTEXT deviceContext = GetMyDeviceContext(device);

NETADAPTER netAdapter = deviceContext->NetAdapter;

PMY_ADAPTER_CONTEXT adapterContext = GetMyAdapterContext(netAdapter);

//
// Optional: set adapter capabilities
//

// Link layer capabilities
...
NetAdapterSetDatapathCapabilities(netAdapter, 
                                  &txCapabilities, 
                                  &rxCapabilities);
...
NetAdapterSetLinkLayerCapabilities(netAdapter,
                                   &linkLayerCapabilities);

NetAdapterSetLinkLayerMtuSize(netAdapter,
                              MY_MAX_PACKET_SIZE - ETHERNET_HEADER_LENGTH);

NetAdapterSetPermanentLinkLayerAddress(netAdapter,
                                       &adapterContext->PermanentAddress);

NetAdapterSetCurrentLinkLayerAddress(netAdapter,
                                     &adapterContext->CurrentAddress);

// Datapath capabilities
...
NetAdapterSetDatapathCapabilities(netAdapter,
                                  &txCapabilities,
                                  &rxCapabilities);

// Power capabilities
...
NetAdapterSetPowerCapabilities(netAdapter,
                               &powerCapabilities);

// Receive scaling capabilities
...
NetAdapterSetReceiveScalingCapabilities(netAdapter,
                                        &receiveScalingCapabilities);

// Hardware offload capabilities
...
NetAdapterOffloadSetChecksumCapabilities(netAdapter,
                                         &checksumCapabilities);
...
NetAdapterOffloadSetLsoCapabilities(netAdapter,
                                    &lsoCapabilities);

//
// Required: start the adapter
//
status = NetAdapterStart(netAdapter);
if(!NT_SUCCESS(status))
{
    return status;
}
```
