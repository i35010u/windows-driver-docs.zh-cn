---
Description: Describes the behavior of the UCSI class extension that implements the UCSI specification in a transport agnostic way.
title: 编写 UCSI 客户端驱动程序
ms.date: 09/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 54359ccbc01a8953cf3406533aeae00cddbfa50d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523646"
---
# <a name="write-a-ucsi-client-driver"></a>编写 UCSI 客户端驱动程序

USB 类型 C 连接器系统软件接口 (UCSI) 驱动程序可用作具有嵌入式控制器 (EC) 的 USB 类型 C 系统控制器驱动程序。

如果您的系统，实现平台策略管理器 (PPM) UCSI 规范中所述，EC 中，通过连接到系统：

- 执行 ACPI 传输_不_需要编写驱动程序。 加载 Microsoft 提供的现成驱动程序，（UcmUcsiCx.sys 和 UcmUcsiAcpiClient.sys）。 (请参阅[UCSI 驱动程序](ucsi.md))。

- 非 ACPI 传输，如 USB、 PCI、 I2C 或 UART，您需要为控制器编写客户端驱动程序。

> 如果您的 USB 类型 C 硬件不具有处理 power 传递 (PD) 状态机的功能，应考虑编写 USB 类型 C 端口控制器驱动程序。 有关详细信息，请参阅[写入 USB 类型 C 端口控制器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)。

从 Windows 10，版本 1809，开始 UCSI (UcmUcsiCx.sys) 的新类扩展已添加，它在传输过程中实现 UCSI 规范无关的方式。 使用极少量的代码，您的驱动程序，这是到 UcmUcsiCx 的客户端，都可与 USB 类型 C 硬件通过非 ACPI 传输通信。 本主题介绍提供 UCSI 类扩展和客户端驱动程序的预期的行为的服务。

**正式规范**
-   [UCSI Intel BIOS 实现](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 3.1 和 USB 类型 C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [UCSI 驱动程序](ucsi.md)

适用于：

- Windows 10 版本 1809

**WDF 版本**

-   KMDF 版本 1.27 版


**重要的 Api**

[UcmUcsiCx 类扩展引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

**Sample**

[UcmUcsiCx 客户端驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

ACPI 部分替换为您所需的总线的实现。

## <a name="ucsi-class-extension-architecture"></a>UCSI 类扩展体系结构
UCSI 类扩展，UcmUcsiCx，可以编写通过使用非 ACPI 传输与其嵌入式控制器进行通信的驱动程序。 控制器驱动程序是 UcmUcsiCx 到客户端驱动程序。 UcmUcsiCx 又是 USB 连接器管理器 (UCM) 的客户端。 因此，UcmUcsiCx 不进行自己的任何策略决策。 相反，它实现了提供 UCM 的策略。 UcmUcsiCx 实现来处理来自客户端驱动程序的平台策略管理器 (PPM) 通知的状态机，并发送命令以实现 UCM 策略决策，从而获得更可靠的问题检测和错误处理。

![UCSI 类扩展体系结构](images/ucsicxarch.png)

**OS 策略管理器 (OPM)**

OS 策略管理器 (OPM) 实现的逻辑，以便与 PPM，UCSI 规范中所述。 OPM 负责：

- UCM 策略转换为 UCSI 命令和 UCSI 到 UCM 通知的通知。
- 发送 UCSI 命令所需的初始化 PPM，检测错误和恢复机制。

**处理 UCSI 命令** 

典型操作涉及多个命令要完成 UCSI complicant 硬件。 例如，假设 GET_CONNECTOR_STATUS 命令。

1. PPM 固件将连接更改通知发送到 UcmUcsiCx/客户端驱动程序。
2. 在响应中，UcmUcsiCx/客户端驱动程序将 GET_CONNECTOR_STATUS 命令发送回 PPM 固件。  
3. PPM 固件执行 GET_CONNECTOR_STATUS 并以异步方式将命令完成通知发送到 UcmUcsiCx/客户端驱动程序。 通知有关包含数据的实际连接状态。
4. UcmUcsiCx/客户端驱动程序处理该状态信息并将 ACK_CC_CI 发送到 PPM 固件。
5. PPM 固件执行 ACK_CC_CI 并以异步方式将命令完成通知发送到 UcmUcsiCx/客户端驱动程序。
6. UcmUcsiCx/客户端驱动程序将视为 GET_CONNECTOR_STATUS 命令完成。

**与平台策略管理器的通信 (PPM)**

UcmUcsiCx 抽象化为 PPM 固件从 OPM 发送 UCSI 命令和 PPM 固件从接收通知的详细信息。 它将 PPM 命令转换为 WDFREQUEST 对象并将其转发到客户端驱动程序。

- PPM 通知

    客户端驱动程序通知有关固件从 PPM 通知 UcmUcsiCx。 该驱动程序提供了包含 CCI UCSI 数据块。 UcmUcsiCx 将通知转发到 OPM 和采取适当措施基于的数据在其他组件。

- Ioctl 到客户端驱动程序

    UcmUcsiCx 将 UCSI 命令 （通过 IOCTL 请求） 发送到客户端驱动程序将发送到 PPM 固件。 该驱动程序负责完成请求后已发送到固件 UCSI 命令。


**处理 power 转换**

客户端驱动程序是电源策略所有者。  

如果客户端驱动程序由于 S0 空闲输入 Dx 状态，WDF 驱动程序为提供 D0 UcmUcsiCx 发送包含到客户端驱动程序的电源管理队列 UCSI 命令 IOCTL 时。 没有来自固件的 PPM 通知因为仍在 S0 空闲，启用 PPM 通知时中 S0 空闲, 的客户端驱动程序应重新输入通电的状态。  

## <a name="before-you-begin"></a>开始之前...

-   确定驱动程序需要编写具体取决于是否您的硬件或固件实现 PD 状态机和传输类型。

    ![有关选择正确的类扩展的决策](images/drivers-c.png)的详细信息，请参阅[USB 类型 C 连接器的开发 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)。  

-   安装 Windows 10 桌面版 （主页、 专业版、 企业版和教育版）。

-   [安装](https://developer.microsoft.com/windows/hardware/windows-driver-kit)最新 Windows 驱动程序工具包 (WDK) 在开发计算机上。 该工具包具有必需的标头文件和库，用于编写客户端驱动程序，具体而言，你将需要：

    -   存根 （stub） 库中，(UcmUcsiCxStub.lib)。 库将转换所做的客户端驱动程序的调用，并将其传递到此类扩展。
    -   标头文件，Ucmucsicx.h。
    - 客户端驱动程序在内核模式下运行，并将绑定到 KMDF 1.27 版库。

-   了解使用 Windows Driver Foundation (WDF)。 推荐阅读的主题：[使用 Windows Driver Foundation 开发驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)、 由 Penny Orwick 和 Smith 专家编写。

## <a name="1-register-your-client-driver-with-ucmucsicx"></a>1.向 UcmUcsiCx 注册客户端驱动程序

在你[ **EVT_WDF_DRIVER_DEVICE_ADD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)实现中， 

1. 设置插和电源管理事件的回调函数之后 ([**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks))，调用[ **UcmUcsiDeviceInitInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitinitialize)来初始化[ **WDFDEVICE_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)不透明结构。 调用将客户端驱动程序与框架相关联。

2. 创建框架设备对象 (WDFDEVICE) 后，调用[ **UcmUcsiDeviceInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitialize.md) UcmUcsiCx 注册客户端驱动程序。

## <a name="2-create-the-ppm-object-with-ucmucsicx"></a>2.创建具有 UcmUcsiCx PPM 对象

中的实现[ **EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)、 后收到的原始和已翻译的资源的列表、 使用的资源来准备硬件。 例如，如果你传输 I2C，读取的硬件资源，以打开通信通道。 接下来，创建一个 PPM 对象。 若要创建对象，需要设置某些配置选项。

1. 在设备上提供的句柄连接器集合。 
   1. 通过调用创建连接器集合[ **UcmUcsiConnectorCollectionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectioncreate)。
   2. 枚举在设备上的连接器，并将其添加到集合，通过调用[ **UcmUcsiConnectorCollectionAddConnector**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectionaddconnector)

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
2. 决定是否想要启用设备控制器。

3. 配置和创建 PPM 对象。
   1. 初始化[ **UCMUCSI_PPM_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/ns-ucmucsippm-ucmucsi-ppm-config)通过提供在步骤 1 中创建的连接器句柄的结构。
   2. 设置**UsbDeviceControllerEnabled**成员添加到在步骤 2 中确定一个布尔值。
   3. WDF_OBJECT_ATTRIBUTES 中设置事件回叫。
   4. 调用[ **UcmUcsiPpmCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmcreate)通过将传递所有已配置的结构。

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
      ## <a name="3-set-up-io-queues"></a>3.设置 IO 队列

UcmUcsiCx 将 UCSI 命令发送到客户端驱动程序将发送到 PPM 固件。 将命令发送这些 IOCTL 请求 WDF 队列中的窗体中。

-  [IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)
-  [IOCTL_UCMUCSI_PPM_GET_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_get_ucsi_data_block)

客户端驱动程序负责创建和注册通过调用该队列到 UcmUcsiCx [ **UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)。 队列不能为电源管理。

UcmUcsiCx 保证，有最多只能包含一个未完成请求 WDF 队列中。 客户端驱动程序还负责完成 WDF 请求已发送到固件 UCSI 命令后。

通常，驱动程序设置了其实现中的队列[ **EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)。

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

此外，还必须调用客户端驱动程序[ **UcmUcsiPpmStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmstart)通知 UcmUcsiCx 驱动程序已准备好接收 IOCTL 请求。  我们建议你进行该调用中的你在[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)创建用于接收 UCSI WDFQUEUE 句柄的命令，通过后[ **UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)。
相反，当驱动程序不希望处理任何更多的请求，它必须调用[ **UcmUcsiPpmStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmstop)。 这是在执行您[ **EVT_WDF_DEVICE_RELEASE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)实现。

## <a name="4-handle-the-ioctl-requests"></a>4.处理 IOCTL 请求

请考虑 USB 类型 C 合作伙伴附加到连接器时，会发生的事件的此示例顺序。

1. PPM 固件确定附加事件，并将通知发送到客户端驱动程序。
2. 客户端驱动程序调用[ **UcmUcsiPpmNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmnotification) UcmUcsiCx 向发送该通知。
3. UcmUcsiCx notfies OPM 状态机，它将获取连接器状态命令发送到 UcmUcsiCx。
4. UcmUcsiCx 创建一个请求，并将发送[IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippmrequestsni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)到客户端驱动程序。
5. 客户端驱动程序处理该请求，并将命令发送到 PPM 固件。 该驱动程序以异步方式完成此请求，并将另一条通知发送到 UcmUcsiCx。
6. 成功的命令完成通知 OPM 状态机读取 （包含连接器的状态信息） 的有效负载，并通知 UCM 类型 C 的附加事件。

在此示例中，负载也指示 power 固件端口合作伙伴之间的传递协商状态中的更改成功。 OPM 状态机将发送另一个 UCSI 命令：获取 PDOs。
类似于获取连接器状态命令，获取 PDOs 命令已成功完成后，通知此事件的 UCM OPM 状态机。

客户端驱动程序的处理程序[EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)类似于此示例代码。 有关处理的请求的信息，请参阅[请求处理程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/request-handlers)

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
