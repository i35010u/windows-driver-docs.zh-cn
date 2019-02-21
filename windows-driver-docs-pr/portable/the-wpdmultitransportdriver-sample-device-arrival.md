---
Description: MultiTransport Device Support
title: MultiTransport 设备支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e43dc9336e483b82615e3f4251bc1a9a20b98f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526906"
---
# <a name="multitransport-device-support"></a>MultiTransport 设备支持


WpdMultiTransportDriver 示例基于 WpdHelloWorldDriver，并且原始的驱动程序的源代码的大部分保持不变。 具体而言，支持对象枚举、 属性和功能的代码包含很少更改或修订。

对 WpdMultiTransportDriver 中的代码修订出现在两个主要方面： 设备到达和 I/O 队列。 在两个文件中找到支持设备到达代码*Device.cpp*并*Driver.cpp*。 支持的 I/O 队列的代码中找到*Driver.cpp*和*Queue.cpp*

## <a name="span-idmultitransportdevice-arrivalspanspan-idmultitransportdevice-arrivalspanspan-idmultitransportdevice-arrivalspanmultitransport-device-arrival"></a><span id="Multitransport_Device-Arrival"></span><span id="multitransport_device-arrival"></span><span id="MULTITRANSPORT_DEVICE-ARRIVAL"></span>Multitransport 设备到达


设备到达代码中找到**CDevice::OnPrepareHardware**方法 (在*Device.cpp*文件) 并在**CDriver::OnDeviceAdd**方法 (在*Driver.cpp*文件)。

中的代码**CDevice::OnPrepareHardware**方法之前初始化 WPD 类扩展完成以下任务。 （最后三个任务设置的选项参数传递给 WPD 类扩展。）

并行的队列是必需的以便**IOCTL\_复合\_传输\_请求 Ioctl**可以正确接收 WPD 类安装程序的设备接口状态更改时。 第二个队列允许传输驱动程序要使用不同 （例如，非并行） 调度模式。 顺序队列是更容易管理，因为 WUDF 仅一次只允许一个请求。 但是，如果您 WPD 的驱动程序能够处理多个并行请求，它不需要辅助队列。

|                                                                       |                                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 任务                                                                  | 描述                                                                                                                                                                                                                      |
| 创建功能的唯一标识符 (FUID)。                         | FUID 是驱动程序将传递给 WPD 类扩展在初始化期间的全局唯一标识符 (GUID) 值。 （此类扩展相关联此 FUID 每个传输协议。）                                   |
| 检索一个指向**IQueueCallbackDeviceIoControl**接口。 | 该驱动程序将任何至类扩展的非-WPD Ioctl 转发通过此指针。                                                                                                                                             |
| 启用 multitransport 模式选项。                                | 此选项会通知其应设置 multitransport framework WPD 类扩展。                                                                                                                                  |
| 设置必要的插 (PnP) 值。                         | 这些值用于配置 multitransport 框架。                                                                                                                                                                 |
| 设置当前流传输的带宽。                                  | 类扩展和复合的驱动程序使用此值 (*WpdComp.dll*)。 复合驱动程序从该扩展插件检索的值，并使用它来确定最佳传输多个传输协议处于活动状态。 |

 

下面的代码示例摘自**CDevice::OnPrepareHardware**方法演示的示例驱动程序创建功能唯一标识符 (FUID) 的方式。 请务必查看前加上此 GUID 创建注释。

```ManagedCPlusPlus
 // ATTENTION: The following GUID value is provided for illustrative
                // purposes only.
                //
                // Rather than hard-coding a GUID value in your driver, the driver
                // must obtain a GUID value from the device. The driver can provision the GUID value on the
                // device (upon first-connect) by
                // using CoCreateGUID and setting that value into non-volatile storage
                // on the device. The same GUID value is then  reported by each
                // of your device&#39;s transports. To avoid a provisioning race condition,
                // always read the value from the device after provisioning. Only
                // provision the GUID one time. Thereafter, always use the value that is provided
                // by the device.
                GUID guidFUID = { 0x245e5e81, 0x2c17, 0x40a4, { 0x8b, 0x10, 0xe9, 0x43, 0xc5, 0x4c, 0x97, 0xb2 } };
```

下面的代码示例摘自**CDevice::OnPrepareHardware**方法显示了上表中的三个剩余任务 (检索**IQueueCallbackDeviceIoControl**指针，启用multitransport 模式，即插即用的值和当前带宽设置。

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

## <a name="span-idmultitransportqueuesspanspan-idmultitransportqueuesspanspan-idmultitransportqueuesspanmultitransport-queues"></a><span id="MultiTransport_Queues"></span><span id="multitransport_queues"></span><span id="MULTITRANSPORT_QUEUES"></span>MultiTransport 队列


WpdHelloWorld 驱动程序示例进程 Ioctl 到单一、 连续队列支持从 WPD 序列化程序。 WpdMultiTransportDriver 驱动程序支持两个队列： 一个并行的队列和顺序的队列。 并行的队列处理多个同时进行的 I/O 请求，而顺序队列处理只在一个请求一次。

中的设备到达代码**CDriver::OnDeviceAdd**方法准备两个队列。 第一个 （或默认） 队列是并行处理每个 IOCTL，然后将其转发到任一第二个 （按顺序） 中的队列驱动程序，或受 WPD 类扩展的另一个队列。

下面的代码示例包含用于创建并行和顺序队列的代码：

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

虽然**CDriver::OnDeviceAdd**方法处理的 I/O 队列创建，而这两个队列中支持的功能的代码中找到*Queue.cpp*文件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





