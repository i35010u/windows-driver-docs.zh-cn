---
Description: MultiTransport 设备支持
title: MultiTransport 设备支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663b9a3f84ad152d90b7e7825be85b6fd88899af
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968299"
---
# <a name="multitransport-device-support"></a>MultiTransport 设备支持


WpdMultiTransportDriver 示例基于 WpdHelloWorldDriver，而原始驱动程序的大部分源代码仍保持不变。 具体而言，支持对象枚举、属性和功能的代码包含非常少的更改或修改。

WpdMultiTransportDriver 中代码的修订出现在两个主要区域：设备到达队列和 i/o 队列。 支持设备到达的代码可在两个文件中找到：*设备 .cpp*和*驱动程序 .cpp*。 支持 i/o 队列的代码位于*驱动程序 .cpp*和*Queue*中

## <a name="span-idmultitransport_device-arrivalspanspan-idmultitransport_device-arrivalspanspan-idmultitransport_device-arrivalspanmultitransport-device-arrival"></a><span id="Multitransport_Device-Arrival"></span><span id="multitransport_device-arrival"></span><span id="MULTITRANSPORT_DEVICE-ARRIVAL"></span>Multitransport 设备到达


设备到达代码在**CDevice：： OnPrepareHardware**方法（在*设备 .cpp*文件中）和**CDriver：： OnDeviceAdd**方法（位于*驱动程序 .cpp*文件中）中找到。

**CDevice：： OnPrepareHardware**方法中的代码在初始化 WPD 类扩展之前完成以下任务。 （最后三个任务设置传递到 WPD 类扩展的选项参数。）

并行队列是必需的，以便在设备接口状态发生更改时，可以从 WPD 类安装程序中正确接收**IOCTL \_ 复合 \_ 传输 \_ 请求 IOCTLs** 。 第二个队列允许传输驱动程序使用不同（例如，非并行）调度模式。 顺序队列更易于管理，因为 WUDF 一次只允许一个请求。 但是，如果 WPD 驱动程序能够并行处理多个请求，则不需要辅助队列。

**任务**：说明

**创建功能唯一标识符（FUID）。**： FUID 是一个全局唯一标识符（GUID）值，驱动程序在初始化过程中会将此值传递给 WPD 类扩展。 （类扩展将此 FUID 与每个传输关联。）

**检索指向**IQueueCallbackDeviceIoControl**接口的指针。**：驱动程序使用此指针将任何非 WPD IOCTLs 转发到类扩展。

**启用 multitransport 模式选项。**：此选项通知 WPD 类扩展它应设置 multitransport 框架。

**设置必需的即插即用（PnP）值。**：这些值用于配置 multitransport 框架。

**设置当前传输带宽。**：此值由类扩展和复合驱动程序（*WpdComp.dll*）使用。 复合驱动程序检索扩展中的值，并在多个传输处于活动状态时使用它来确定最佳传输。


 

以下来自**CDevice：： OnPrepareHardware**方法的代码示例演示示例驱动程序如何创建功能唯一标识符（FUID）。 请确保在创建此 GUID 之前查看注释。

```ManagedCPlusPlus
 // ATTENTION: The following GUID value is provided for illustrative
                // purposes only.
                //
                // Rather than hard-coding a GUID value in your driver, the driver
                // must obtain a GUID value from the device. The driver can provision the GUID value on the
                // device (upon first-connect) by
                // using CoCreateGUID and setting that value into non-volatile storage
                // on the device. The same GUID value is then  reported by each
                // of your device's transports. To avoid a provisioning race condition,
                // always read the value from the device after provisioning. Only
                // provision the GUID one time. Thereafter, always use the value that is provided
                // by the device.
                GUID guidFUID = { 0x245e5e81, 0x2c17, 0x40a4, { 0x8b, 0x10, 0xe9, 0x43, 0xc5, 0x4c, 0x97, 0xb2 } };
```

以下来自**CDevice：： OnPrepareHardware**方法的代码示例显示了上表中的三个剩余任务（检索**IQueueCallbackDeviceIoControl**指针、启用 Multitransport 模式、设置 PnP 值和当前带宽。

```ManagedCPlusPlus
     if (hr == S_OK)
                {
                    m_pWpdBaseDriver->m_pQueueCallback = NULL;

                    HRESULT hrTemp = m_pPortableDeviceClassExtension->QueryInterface(
                        __uuidof(IQueueCallbackDeviceIoControl),
                        (void**)&m_pWpdBaseDriver->m_pQueueCallback
                        );
                    CHECK_HR(hrTemp, "Failed to obtain IQueueCallbackDeviceIoControl interface from class extension");

                    if (hrTemp == S_OK)
                    {
                        // Enable the Multi-Transport Mode option
                        hr = pOptions->SetBoolValue(WPD_CLASS_EXTENSION_OPTIONS_MULTITRANSPORT_MODE, TRUE);
                        CHECK_HR(hr, "Failed to enable multi-transport mode");

                        // Create a PnP ID value collection
                        if (hr == S_OK)
                        {
                            hr = CreateIDValues(DEVICE_MANUFACTURER_VALUE,
                                                DEVICE_MODEL_VALUE,
                                                DEVICE_FIRMWARE_VERSION_VALUE,
                                                &guidFUID,
                                                &pIDs);
                            CHECK_HR(hr, "Failed to Create the ID value collection");
                        }

                        // Add the PnP ID value collection to the options
                        if (hr == S_OK)
                        {
                            hr = pOptions->SetIPortableDeviceValuesValue(WPD_CLASS_EXTENSION_OPTIONS_DEVICE_IDENTIFICATION_VALUES, pIDs);
                            CHECK_HR(hr, "Failed to set WPD_CLASS_EXTENSION_OPTIONS_DEVICE_IDENTIFICATION_VALUES");
                        }

                        // Add the transport bandwidth (in kilobits per second units) to the options
                        // (0 indicates bandwidth unknown)
                        if (hr == S_OK)
                        {
                            // Set the transport bandwidth (optional)
                            hr = pOptions->SetUnsignedIntegerValue(WPD_CLASS_EXTENSION_OPTIONS_TRANSPORT_BANDWIDTH, 0L);
                            CHECK_HR(hr, "Failed to set WPD_CLASS_EXTENSION_OPTIONS_TRANSPORT_BANDWIDTH");
                        }
                    }
                }
```

## <a name="span-idmultitransport_queuesspanspan-idmultitransport_queuesspanspan-idmultitransport_queuesspanmultitransport-queues"></a><span id="MultiTransport_Queues"></span><span id="multitransport_queues"></span><span id="MULTITRANSPORT_QUEUES"></span>MultiTransport 队列


WpdHelloWorld driver 示例支持单顺序队列，用于处理 WPD 序列化程序中的 IOCTLs。 WpdMultiTransportDriver 驱动程序支持两个队列：并行队列和顺序队列。 并行队列处理多个同时进行的 i/o 请求，而顺序队列一次只处理一个请求。

**CDriver：： OnDeviceAdd**方法中的设备到达代码准备两个队列。 第一个（或默认）队列是一个并行队列，用于处理每个 IOCTL，然后将其转发到驱动程序中的第二个（顺序）队列，或转发到 WPD 类扩展所支持的另一个队列。

下面的代码示例包含创建并行和顺序队列的代码：

```ManagedCPlusPlus
        //
        // Create the default queue callback object
        //
        CComPtr<IUnknown> pIUnknown;
        if(S_OK == hr)
        {
            hr = CDefaultQueue::CreateInstance(&pIUnknown);
        }

        //
        // Configure the default queue.
        //
        if(S_OK == hr)
        {
            CComPtr<IWDFIoQueue> pDefaultQueue;
            hr = pIWDFDevice->CreateIoQueue(
                              pIUnknown,
                              TRUE,                         // bDefaultQueue
                              WdfIoQueueDispatchParallel,
                              TRUE,                         // bPowerManaged
                              FALSE,                        // bAllowZeroLengthRequests
                              &pDefaultQueue);
        }
        pIUnknown = NULL;

        //
        // Create the WPD queue callback object
        //
        if(S_OK == hr)
        {
            hr = CQueue::CreateInstance(&pIUnknown);
        }

        //
        // Configure the WPD queue.
        //
        if(S_OK == hr)
        {
            hr = pIWDFDevice->CreateIoQueue(
                              pIUnknown,
                              FALSE,                        // bDefaultQueue
                              WdfIoQueueDispatchSequential,
                              TRUE,                         // bPowerManaged
                              FALSE,                        // bAllowZeroLengthRequests
                              &pWpdBaseDriver->m_pWpdQueue);
        }
```

当**CDriver：： OnDeviceAdd**方法处理 i/o 队列的创建时，在*队列 .cpp*文件中可找到支持这两个队列中的功能的代码。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





