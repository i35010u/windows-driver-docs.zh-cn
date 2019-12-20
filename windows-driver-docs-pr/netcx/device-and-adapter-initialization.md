---
title: 设备和适配器初始化
description: 设备和适配器初始化
ms.assetid: EBBEF0FB-6CDB-4899-AAE9-71812EE20AFB
keywords:
- NetAdapterCx 设备初始化，NetCx 设备初始化，NetAdapterCx 适配器初始化，NetCx 适配器初始化
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: fa223b69e656015ff82bcdaebc79283eb52df292
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210887"
---
# <a name="device-and-adapter-initialization"></a>设备和适配器初始化

本主题介绍 NetAdapterCx 客户端驱动程序初始化和启动 WDFDEVICE 和 GET-NETADAPTER 对象的步骤。 有关这些对象及其关系的详细信息，请参阅[NetAdapterCx 对象的摘要](summary-of-netadaptercx-objects.md)。

## <a name="evt_wdf_driver_device_add"></a>EVT_WDF_DRIVER_DEVICE_ADD

NetAdapterCx 客户端驱动程序在从其[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程调用[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)时，会注册其[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

在[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)中，NetAdapterCx 客户端驱动程序应按顺序执行以下操作：

1. 调用[**NetDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nf-netdevice-netdeviceinitconfig)。

    ```C++
    status = NetDeviceInitConfig(DeviceInit);
    if (!NT_SUCCESS(status)) 
    {
        return status;
    }
    ```

2. 调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。 

    > [!TIP]
    > 如果你的设备支持多个 GET-NETADAPTER，我们建议你将指针存储在设备上下文中的每个适配器。

3. 创建 GET-NETADAPTER 对象。 为此，客户端将调用[**NetAdapterInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterinitallocate)，然后调用**NetAdapterInitSetXxx**方法来 initailize 适配器的特性。 最后，客户端调用[**NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)。 

    下面的示例演示客户端驱动程序如何初始化 GET-NETADAPTER 对象。 请注意，在此示例中简化了错误处理。

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
    NET_ADAPTER_DATAPATH_CALLBACKS datapathCallbacks;
    NET_ADAPTER_DATAPATH_CALLBACKS_INIT(&datapathCallbacks,
                                        MyEvtAdapterCreateTxQueue,
                                        MyEvtAdapterCreateRxQueue);
    NetAdapterInitSetDatapathCallbacks(adapterInit,
                                       datapathCallbacks);
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

（可选）可以向 GET-NETADAPTER 对象添加上下文空间。 由于可以在任何 WDF 对象上设置上下文，因此可以为 WDFDEVICE 和 GET-NETADAPTER 对象添加单独的上下文空间。 在步骤3的示例中，客户端将 `MY_ADAPTER_CONTEXT` 添加到 GET-NETADAPTER 对象。 有关详细信息，请参阅[框架对象上下文空间](../wdf/framework-object-context-space.md)。

建议你在 WDFDEVICE 的上下文中将设备相关数据以及与网络相关的数据（例如链接层地址）放入 GET-NETADAPTER 上下文中。 如果要移植现有的 NDIS 1.x 驱动程序，则可能会有单个 MiniportAdapterContext 将与网络相关的数据和与设备相关的数据组合到一个数据结构中。 若要简化移植过程，只需将整个结构转换为 WDFDEVICE 上下文，并使 GET-NETADAPTER 的上下文成为指向 WDFDEVICE 的上下文的小型结构。

你可以选择提供两个对[**NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)方法的回调：

* [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)
* [*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)

有关在这些回调的实现中提供的内容的详细信息，请参阅各个参考页。

## <a name="evt_wdf_device_prepare_hardware"></a>EVT_WDF_DEVICE_PREPARE_HARDWARE

许多 NetAdapterCx 客户端驱动程序都在其[*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数内启动其适配器，这在[移动宽带类扩展客户端驱动程序](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)中明显例外。 若要注册*EVT_WDF_DEVICE_PREPARE_HARDWARE*回调函数，NetAdapterCx 客户端驱动程序必须调用[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)。 

在[*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)中，除其他硬件准备任务外，客户端驱动程序还必须调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)。 在执行此操作之前，驱动程序可以选择设置适配器的功能。

下面的示例演示客户端驱动程序如何启动 GET-NETADAPTER 对象。 请注意，设置每个适配器功能方法所需的代码为了简洁明了和清晰，并简化了错误处理。

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
                                    ...
NetAdapterOffloadSetRscCapabilities(netAdapter,
                                    &rscCapabilities);

//
// Required: start the adapter
//
status = NetAdapterStart(netAdapter);
if(!NT_SUCCESS(status))
{
    return status;
}
```
