---
Description: 描述以不可知的方式实现 UCSI 规范的 UCSI 类扩展的行为。
title: 编写 UCSI 客户端驱动程序
ms.date: 09/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: b059d03672d8c08d894229997d3b31239bd95971
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841681"
---
# <a name="write-a-ucsi-client-driver"></a>编写 UCSI 客户端驱动程序

USB 类型 C 连接器系统软件接口（UCSI）驱动程序充当带有嵌入式控制器（EC）的 USB 类型 C 系统的控制器驱动程序。

如果你的系统实现平台策略管理器（PPM），如 UCSI 规范中所述，在连接到系统的 EC 中：

- ACPI 传输，_无需编写_驱动程序。 加载 Microsoft 提供的内置驱动程序，（UcmUcsiCx 和 UcmUcsiAcpiClient）。 （请参阅[UCSI 驱动程序](ucsi.md)）。

- 非 ACPI 传输（如 USB、PCI、I2C 或 UART）需要为控制器编写客户端驱动程序。

> 如果 USB 类型 C 硬件不具备处理电源交付（PD）状态机的能力，请考虑写入 USB 类型 C 端口控制器驱动程序。 有关详细信息，请参阅[编写 USB 类型 C 端口控制器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)。

从 Windows 10 1809 版开始，添加了一个新的 UCSI （UcmUcsiCx）类扩展，该扩展以与传输无关的方式实现 UCSI 规范。 只需编写极少量的代码，驱动程序（即 UcmUcsiCx 的客户端）即可通过非 ACPI 传输来与 USB 类型 C 硬件通信。 本主题介绍 UCSI 类扩展提供的服务，以及客户端驱动程序的预期行为。

**官方规范**
-   [UCSI 的 Intel BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 3.1 和 USB 类型-C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [UCSI 驱动程序](ucsi.md)

适用范围：

- Windows 10 版本 1809

**WDF 版本**

-   KMDF 版本1.27


**重要的 API**

[UcmUcsiCx 类扩展参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

**范例**

[UcmUcsiCx 客户端驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

将 ACPI 部分替换为所需总线的实现。

## <a name="ucsi-class-extension-architecture"></a>UCSI 类扩展体系结构
UCSI class extension UcmUcsiCx 允许使用非 ACPI 传输来编写与其嵌入式控制器通信的驱动程序。 控制器驱动程序是 UcmUcsiCx 的客户端驱动程序。 UcmUcsiCx 正在将客户端转到 USB 连接器管理器（UCM）。 因此，UcmUcsiCx 不会做出自己的任何策略决策。 相反，它会实现 UCM 提供的策略。 UcmUcsiCx 实现了用于处理来自客户端驱动程序的平台策略管理器（PPM）通知的状态机，并发送命令来实现 UCM 策略决策，从而实现更可靠的问题检测和错误处理。

![UCSI 类扩展体系结构](images/ucsicxarch.png)

**OS 策略管理器（OPM）**

操作系统策略管理器（OPM）实现逻辑以与 PPM 交互，如 UCSI 规范中所述。 OPM 负责：

- 将 UCM 策略转换为 UCSI 命令，并将 UCSI 通知转换为 UCM 通知。
- 发送初始化 PPM、检测错误和恢复机制所需的 UCSI 命令。

**处理 UCSI 命令** 

典型的操作涉及 UCSI-complicant 硬件完成的几个命令。 例如，让我们考虑 GET_CONNECTOR_STATUS 命令。

1. PPM 固件向 UcmUcsiCx/客户端驱动程序发送连接更改通知。
2. 作为响应，UcmUcsiCx/客户端驱动程序将 GET_CONNECTOR_STATUS 命令发送回 PPM 固件。  
3. PPM 固件执行 GET_CONNECTOR_STATUS，并以异步方式将命令完成通知发送到 UcmUcsiCx/客户端驱动程序。 该通知包含有关实际连接状态的数据。
4. UcmUcsiCx/客户端驱动程序处理该状态信息，并将 ACK_CC_CI 发送到 PPM 固件。
5. PPM 固件执行 ACK_CC_CI，并以异步方式将命令完成通知发送到 UcmUcsiCx/客户端驱动程序。
6. UcmUcsiCx/客户端驱动程序会将 GET_CONNECTOR_STATUS 命令视为已完成。

**与平台策略管理器（PPM）通信**

UcmUcsiCx 将从 OPM 到 PPM 固件发送 UCSI 命令和从 PPM 固件接收通知的详细信息。 它将 PPM 命令转换为 WDFREQUEST 对象，并将其转发到客户端驱动程序。

- PPM 通知

    客户端驱动程序通过固件通知 UcmUcsiCx 有关 PPM 通知的信息。 驱动程序提供包含 CCI 的 UCSI 数据块。 UcmUcsiCx 将通知转发到 OPM 和其他组件，这些组件根据数据采取适当的操作。

- IOCTLs 到客户端驱动程序

    UcmUcsiCx 将 UCSI 命令（通过 IOCTL 请求）发送到客户端驱动程序以发送到 PPM 固件。 在将 UCSI 命令发送到固件后，该驱动程序负责完成该请求。


**处理电源转换**

客户端驱动程序是电源策略所有者。  

如果客户端驱动程序由于 S0 空闲而进入 Dx 状态，则当 UcmUcsiCx 将包含 UCSI 命令的 IOCTL 发送到客户端驱动程序的受管理队列时，WDF 会将驱动程序带入 D0。 由于固件处于 PPM 空闲状态，因此仍启用 PPM 通知，因此，S0 中的客户端驱动程序应重新进入 "已通电" 状态。  

## <a name="before-you-begin"></a>开始之前 。

-   确定需要写入的驱动程序类型，具体取决于你的硬件或固件是否实现了 PD 状态机和传输。

    ![决定如何选择正确的类扩展](images/drivers-c.png) 有关详细信息，请参阅[开发适用于 USB 类型 C 连接器的 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)。  

-   安装适用于桌面版的 Windows 10 （家庭版、专业版、企业版和教育版）。

-   在开发计算机上[安装](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)最新的 Windows 驱动程序工具包（WDK）。 工具包具有写入客户端驱动程序所需的头文件和库，具体而言，你将需要：

    -   存根库（UcmUcsiCxStub）。 库转换客户端驱动程序发出的调用，并将其传递给类扩展。
    -   标头文件 Ucmucsicx。
    - 客户端驱动程序在内核模式下运行并绑定到 KMDF 1.27 库。

-   熟悉 Windows Driver Foundation （WDF）。 建议读物：[开发带有 Windows Driver Foundation 的驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)（由 "Orwick" 和 "专家 Smith" 编写）。

## <a name="1-register-your-client-driver-with-ucmucsicx"></a>1. 将客户端驱动程序注册到 UcmUcsiCx

在[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)实现中， 

1. 设置即插即用和电源管理事件回调函数（[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)）后，调用[**UcmUcsiDeviceInitInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitinitialize)来初始化[**WDFDEVICE_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)不透明结构。 调用将客户端驱动程序与框架相关联。

2. 创建框架设备对象（WDFDEVICE）后，调用[**UcmUcsiDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitialize.md) ，将客户端驱动程序注册到 UcmUcsiCx。

## <a name="2-create-the-ppm-object-with-ucmucsicx"></a>2. 通过 UcmUcsiCx 创建 PPM 对象

在[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)的实现中，在收到原始资源和已翻译资源的列表后，请使用资源来准备硬件。 例如，如果你的传输为 I2C，请阅读硬件资源以打开信道。 接下来，创建 PPM 对象。 若要创建对象，需要设置某些配置选项。

1. 提供设备上连接器集合的句柄。 
   1. 通过调用[**UcmUcsiConnectorCollectionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectioncreate)创建连接器集合。
   2. 枚举设备上的连接器，并通过调用 UcmUcsiConnectorCollectionAddConnector 将其添加到[集合](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectionaddconnector)

      ```cpp
      // Create the connector collection.

      UCMUCSI_CONNECTOR_COLLECTION* ConnectorCollectionHandle;

      status = UcmUcsiConnectorCollectionCreate(Device, //WDFDevice
               WDF_NO_OBJECT_ATTRIBUTES,
               ConnectorCollectionHandle);

      // Enumerate the connectors on the device.
      // ConnectorId of 0 is reserved for the parent device.
      // In this example, we assume the parent has no children connectors.

      UCMUCSI_CONNECTOR_INFO_INIT(&connectorInfo);
      connectorInfo.ConnectorId = 0;

      status = UcmUcsiConnectorCollectionAddConnector ( &ConnectorCollectionHandle,
                   &connectorInfo);
      ```
2. 决定是否要启用设备控制器。

3. 配置和创建 PPM 对象。
   1. 通过提供在步骤1中创建的连接器句柄来初始化[**UCMUCSI_PPM_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/ns-ucmucsippm-_ucmucsi_ppm_config)结构。
   2. 将**UsbDeviceControllerEnabled**成员设置为在步骤2中确定的布尔值。
   3. 在 WDF_OBJECT_ATTRIBUTES 中设置事件回调。
   4. 通过传递所有配置的结构来调用[**UcmUcsiPpmCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmcreate) 。

      ```cpp
      UCMUCSIPPM ppmObject = WDF_NO_HANDLE;
      PUCMUCSI_PPM_CONFIG UcsiPpmConfig;
      WDF_OBJECT_ATTRIBUTES attrib;

      UCMUCSI_PPM_CONFIG_INIT(UcsiPpmConfig, ConnectorCollectionHandle);

      UcsiPpmConfig->UsbDeviceControllerEnabled = TRUE;

      WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attrib, Ppm);
      attrib->EvtDestroyCallback = &EvtObjectContextDestroy;

      status = UcmUcsiPpmCreate(wdfDevice, UcsiPpmConfig, &attrib, &ppmObject);
      ```
      ## <a name="3-set-up-io-queues"></a>3. 设置 IO 队列

UcmUcsiCx 将 UCSI 命令发送到客户端驱动程序，以发送到 PPM 固件。 命令在 WDF 队列中以这些 IOCTL 请求的形式进行发送。

-  [IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)
-  [IOCTL_UCMUCSI_PPM_GET_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_get_ucsi_data_block)

客户端驱动程序负责通过调用[**UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)创建该队列并将其注册到 UcmUcsiCx。 必须对队列进行电源管理。

UcmUcsiCx 保证 WDF 队列中最多只能有一个未完成的请求。 在将 UCSI 命令发送到固件之后，客户端驱动程序还负责完成 WDF 请求。

通常，驱动程序会在其[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)实现中设置队列。

```cpp
WDFQUEUE UcsiCommandRequestQueue = WDF_NO_HANDLE;
WDF_OBJECT_ATTRIBUTES attrib;
WDF_IO_QUEUE_CONFIG queueConfig;

WDF_OBJECT_ATTRIBUTES_INIT(&attrib);
attrib.ParentObject = GetObjectHandle();

// In this example, even though the driver creates a sequential queue, 
// UcmUcsiCx guarantees that will not send another request 
// until the previous one has been completed.


WDF_IO_QUEUE_CONFIG_INIT(&queueConfig, WdfIoQueueDispatchSequential);

// The queue must be power-managed.

queueConfig.PowerManaged = WdfTrue;
queueConfig.EvtIoDeviceControl = EvtIoDeviceControl;

status = WdfIoQueueCreate(device, &queueConfig, &attrib, &UcsiCommandRequestQueue);

UcmUcsiPpmSetUcsiCommandRequestQueue(ppmObject, UcsiCommandRequestQueue);
```

此外，客户端驱动程序还必须调用[**UcmUcsiPpmStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmstart)来通知 UcmUcsiCx 驱动程序已准备好接收 IOCTL 请求。  建议你在创建 WDFQUEUE 句柄以便接收 UCSI 命令后，在[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)中进行此[**调用。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)
相反，当驱动程序不希望处理更多请求时，它必须调用[**UcmUcsiPpmStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmstop)。 请在[**EVT_WDF_DEVICE_RELEASE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)实现中执行此操作。

## <a name="4-handle-the-ioctl-requests"></a>4. 处理 IOCTL 请求

请考虑此示例序列，这是在将 USB 类型 C 伙伴附加到连接器时发生的事件的序列。

1. PPM 固件确定附加事件，并向客户端驱动程序发送通知。
2. 客户端驱动程序调用[**UcmUcsiPpmNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmnotification)将该通知发送到 UcmUcsiCx。
3. UcmUcsiCx notfies OPM 状态机，并向 UcmUcsiCx 发送获取连接器状态命令。
4. UcmUcsiCx 创建请求并向客户端驱动程序发送[IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block) 。
5. 客户端驱动程序处理请求并将命令发送到 PPM 固件。 驱动程序以异步方式完成此请求，并向 UcmUcsiCx 发送另一个通知。
6. 成功完成命令通知后，OPM 状态机将读取有效负载（包含连接器状态信息），并通知类型 C 附加事件的 UCM。

在此示例中，负载还表明固件和端口伙伴之间的电源传送协商状态更改成功。 OPM 状态机发送另一个 UCSI 命令： Get PDOs。
与 "获取连接器状态" 命令类似，Get PDOs 命令成功完成后，OPM 状态机将通知 UCM 此事件。

[EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)的客户端驱动程序的处理程序类似于此示例代码。 有关处理请求的信息，请参阅[请求处理程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/request-handlers)

```cpp
void EvtIoDeviceControl(
    _In_ WDFREQUEST Request,
    _In_ ULONG IoControlCode
    )
{
...
    switch (IoControlCode)
    {
    case IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK:
        EvtSendData(Request);
        break;

    case IOCTL_UCMUCSI_PPM_GET_UCSI_DATA_BLOCK:
        EvtReceiveData(Request);
        break;

    default:
        status = STATUS_NOT_SUPPORTED;
        goto Exit;
    }

    status = STATUS_SUCCESS;

Exit:

    if (!NT_SUCCESS(status))
    {
        WdfRequestComplete(Request, status);
    }

}

VOID EvtSendData(
    WDFREQUEST Request
    )
{
    NTSTATUS status;
    PUCMUCSI_PPM_SEND_UCSI_DATA_BLOCK_IN_PARAMS inParams;

    status = WdfRequestRetrieveInputBuffer(Request, sizeof(*inParams),
        reinterpret_cast<PVOID*>(&inParams), nullptr);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    // Build a UCSI command request and send to the PPM firmware.

Exit:
    WdfRequestComplete(Request, status);
}

VOID EvtReceiveData(
    WDFREQUEST Request
    )
{

    NTSTATUS status;

    PUCMUCSI_PPM_GET_UCSI_DATA_BLOCK_IN_PARAMS inParams;
    PUCMUCSI_PPM_GET_UCSI_DATA_BLOCK_OUT_PARAMS outParams;

    status = WdfRequestRetrieveInputBuffer(Request, sizeof(*inParams),
        reinterpret_cast<PVOID*>(&inParams), nullptr);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    status = WdfRequestRetrieveOutputBuffer(Request, sizeof(*outParams),
        reinterpret_cast<PVOID*>(&outParams), nullptr);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    // Receive data from the PPM firmware.
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }
    WdfRequestSetInformation(Request, sizeof(*outParams));

Exit:
    WdfRequestComplete(Request, status);
}
```
