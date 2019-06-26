---
Description: 本主题介绍发出选择接口请求以激活一项备用设置 USB 接口中的步骤。
title: 如何在 USB 界面中选择备用设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fed908434647b4e32607da1e4857947a9be7984
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368811"
---
# <a name="how-to-select-an-alternate-setting-in-a-usb-interface"></a>如何在 USB 界面中选择备用设置


本主题介绍发出选择接口请求以激活一项备用设置 USB 接口中的步骤。 客户端驱动程序必须选择 USB 配置后发出此请求。 默认情况下，选择一个配置，还会激活该配置中每个接口中的第一个备用设置。

每个 USB 配置必须支持一个或多个多个 USB 接口。 每个接口公开用于传输数据传入和传出设备的一个或多个终结点。 USB 接口必须有设备定义，*接口索引*用于标识接口。 接口还必须具有一个或多个*备用设置*组接口的终结点。 作为设备配置的一部分，客户端驱动程序必须选择一个替代设置的界面中。 因为可以在备用设置之间共享的终结点，只有一种设置可以处于活动状态在给定的时间。 备用设置处于活动状态后，其终结点会变得可用的数据传输。

对于多个接口设备，两个接口可以在某一时刻处于活动状态。 客户端驱动程序必须激活一项备用设置中的每个接口。 接口，因此，每个同时进行数据传输可以执行的每个接口间不共享终结点。

设备定义和调用的编号标识备用的设置*设置索引*。 调用索引 0 处的备用设置*默认备用设置*本文档中设置。 中介绍了备用设置[ **USB\_界面\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)结构。 该结构包含设置与之关联的接口索引和设置所定义的终结点的数量。 它还包含有关接口的功能所遵循的类规范的信息。 终结点分组的方式取决于设备的功能。

例如，一个接口公开两个同步和通过三种备用设置 （索引 0，1，2） 的两个大容量终结点。 备用设置 0 不定义任何终结点;备用设置 1 定义大容量终结点;备用设置 2 定义等时终结点。 备用设置 0 具有任何终结点，客户端驱动程序可以选择此设置以禁用数据传输，以便节省带宽。 其他设置的任何一个处于活动状态，设备已准备就绪的数据传输。 可以使用备用设置 1 将大容量数据传输。 在设备处于流模式时，可以选择备用设置 2。 因此，替代设置，使客户端驱动程序更改设备配置按需的灵活性。 在此示例中，客户端驱动程序可以切换到流式处理，只需通过选择一项备用设置设备功能从大容量传输。

此外可以使用备用设置设置带宽要求。 有关示例，请参阅[USB 设备布局](usb-device-layout.md)。

Windows Driver Foundation (WDF) 提供了中的方法[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)并[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)客户端驱动程序可以调用以选择其他备用设置。 通过指定的设置索引、 接口描述符设置，或通过提交包含请求 URB KMDF 客户端驱动程序可以选择的设置。 UMDF 客户端驱动程序仅可通过指定其设置索引选择一项备用设置。

选择配置请求成功完成后，将停用之前处于活动状态的替代设置。

## <a name="what-you-need-to-know"></a>你需要了解的内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>系统必备

客户端驱动程序可以选择一项备用设置之前，请确保满足这些要求：

-   客户端驱动程序必须已创建的 framework USB 目标设备对象。

    -   KMDF 客户端驱动程序必须通过调用获取 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法。 详细信息，请参阅"设备源代码"中[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)。
    -   UMDF 客户端驱动程序必须获取[ **IWDFUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)通过查询框架目标设备对象的指针。 有关详细信息，请参阅"[**IPnpCallbackHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"中[了解 USB 客户端驱动程序代码结构 (UMDF)](understanding-the-umdf-template-code-for-usb.md)

    如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码执行这些任务。 模板代码获取目标设备对象的句柄，并将存储在设备上下文中。

-   设备必须具有活动的配置。
    -   KMDF 客户端驱动程序必须调用[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)方法。
    -   UMDF 客户端驱动程序，该框架选择该配置中的第一个配置和每个接口的默认备用设置。

    如果使用的 USB 模板，该代码将在每个接口中选择的第一个配置和默认值替代设置。

<a name="instructions"></a>说明
------------

### <a name="select-an-alternate-setting---kmdf-client-driver"></a>选择一项备用设置-KMDF 客户端驱动程序

1.  获取 WDFUSBINTERFACE 句柄已替代设置的接口。

    若要获取句柄，请先获取所选配置的接口的数量通过调用[ **WdfUsbTargetDeviceGetNumInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetnuminterfaces) ，然后枚举在循环中的接口。 在每个迭代调用[ **WdfUsbTargetDeviceGetInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)方法和增量索引 （从零开始）。

    **请注意**  设备枚举期间 USB 驱动程序堆栈将数字赋给的替代设置。 接口数字是从零开始和顺序。 这些数字可能不同于设备定义设置索引。 若要获取设备定义设置索引，请调用[ **WdfUsbInterfaceGetInterfaceNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetinterfacenumber)方法。

     

2.  通过调用启动选择接口请求[ **WdfUsbInterfaceSelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)方法。 在中*Params*参数的调用中，选择以下选项之一：

    -   指定 USB 驱动程序堆栈分配的替代设置编号。 通常情况下，您将其传递相同的索引在步骤 1 中用于枚举设置。
    -   指定描述替代设置的接口描述符的指针。 该驱动程序然后可以通过调用枚举接口中的替代设置时获取接口描述符[ **WdfUsbInterfaceGetDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)方法。 该驱动程序枚举完成后，获取有关所有中枚举的替代设置的信息[ **USB\_界面\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)结构。
    -   指定指向包含选择接口请求所需的所有信息 URB 的指针。

        1.  分配的数组[ **USBD\_界面\_列表\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/ns-usbdlib-_usbd_interface_list_entry)结构。 此数组中元素的数目取决于所选的配置中的接口的数量。 有关初始化此数组的信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。
        2.  分配[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)选择接口请求通过调用[ **USBD\_SelectInterfaceUrbAllocateAndBuild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)例程。 在此调用中指定的接口列表数组和选择一种配置后获取的配置句柄。 可以通过调用获取该句柄[ **WdfUsbTargetDeviceWdmGetConfigurationHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicewdmgetconfigurationhandle)方法。
        3.  调用[ **WdfUsbInterfaceSelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)并指定 URB。

        **WDM 驱动程序：  **若要提交 URB，将 URB IRP，与相关联，并提交到 USB 驱动程序堆栈 IRP。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

    在列表中的选项用于指定选择条件灵活地提供客户端驱动程序。 如果您已知道替代设置的终结点功能，请在列表中选择第一个选项 （使用备用设置数量）。 否则，请选择指定接口描述符的第二个选项。 检查[ **USB\_界面\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)结构的所有替代设置。 对于每个设置，请枚举其终结点和终结点类型，最大数据包大小，例如其特征等。 找到所需的数据传输的终结点集后，调用[ **WdfUsbInterfaceSelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)通过指定指向该接口描述符的指针。 通常情况下，您将不需要使用第三个选项，除非您是可以仅将请求发送到 USB 驱动程序堆栈通过提交 URBs WDM 基于客户端驱动程序。

    USB 驱动程序堆栈基于客户端驱动程序提供的信息，然后生成标准控件请求 （设置接口） 并将其发送到设备。 如果请求成功完成，USB 驱动程序堆栈获取管道句柄的替代设置的终结点。

    选择后一项备用设置，客户端驱动程序始终必须获取终结点的管道句柄中新的设置。 如果不这样做可能会导致驱动程序以使用过时的管道句柄发送数据传输请求。 有关检索管道句柄的信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

```cpp
NTSTATUS  FX3SelectInterfaceSetting(  
    _In_ WDFDEVICE Device,
    _In_ UCHAR SettingIndex)

{
    NTSTATUS                 status;  
    PDEVICE_CONTEXT          pDeviceContext;  
    WDF_OBJECT_ATTRIBUTES               pipeAttributes;

    WDF_USB_INTERFACE_SELECT_SETTING_PARAMS settingParams;

    PAGED_CODE();  

    pDeviceContext = GetDeviceContext(Device);

    if (pDeviceContext->UsbInterface == NULL)
    {
        status = USBD_STATUS_BAD_NUMBER_OF_INTERFACES;
        goto Exit;
    }

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&pipeAttributes, PIPE_CONTEXT);  

    pipeAttributes.EvtCleanupCallback = FX3EvtPipeContextCleanup;

    WDF_USB_INTERFACE_SELECT_SETTING_PARAMS_INIT_SETTING (&settingParams, SettingIndex);

    status = WdfUsbInterfaceSelectSetting (
        pDeviceContext->UsbInterface,
        &pipeAttributes,
        &settingParams);

    if (status != STATUS_SUCCESS)
    {
        goto Exit;
    }

    if (WdfUsbInterfaceGetNumConfiguredPipes (pDeviceContext->UsbInterface) > 0)
    {
        status = FX3EnumeratePipes (Device);

        if (status != STATUS_SUCCESS)
        {
            goto Exit;
        }
    }

Exit:
    return status;
}
```

### <a name="select-an-alternate-setting---umdf-client-driver"></a>选择一项备用设置-UMDF 客户端驱动程序

1.  获取通过调用支持活动配置的 USB 接口的数量[ **IWDFUsbTargetDevice::GetNumInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)方法。
2.  获取[ **IWDFUsbInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)配置中每个接口的指针。

    通过调用枚举所有接口[ **IWDFUsbTargetDevice::RetrieveUsbInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)中循环直至该函数返回空值的方法。 每次迭代时，便会递增成员索引 （从零开始）。 循环检索[ **IWDFUsbInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)指向枚举的所有接口的指针。

3.  对于每个接口，通过调用获取 WinUSB 句柄[ **IWDFUsbInterface::GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)。 下一步需要使用此句柄。
4.  调用[ **WinUsb\_GetAssociatedInterface** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface)获取接口的句柄。 在中*AssociatedInterfaceIndex*参数，在步骤 2 中指定的索引。
5.  确定备用界面中设置的数量。

    调用[ **WinUsb\_QueryInterfaceSettings** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)函数在循环中，并递增 （从零开始） 在每次迭代中的索引。 当枚举所有设置时，该函数将返回错误\_否\_详细\_项。 该函数还返回每个设置的接口描述符。

6.  通过使用在获得的值**bNumEndpoints**的每个成员接口描述符，并枚举其终结点。 检查终结点描述符并确定哪些设置满足你的要求。
7.  通过调用启动选择接口请求[ **WinUsb\_SetCurrentAlternateSetting** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting)函数。 在调用中，指定在步骤 4 中的索引与关联的替代设置号。
8.  发布接口句柄通过调用在步骤 4 中获得[ **WinUsb\_免费**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)函数。
9.  释放通过调用在步骤 3 中获得 WinUSB 句柄[ **WinUsb\_免费**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)函数。
10. 如果已完成使用[ **IWDFUsbInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)方法，释放在步骤 2 中检索到的所有接口指针。

<a name="remarks"></a>备注
-------

KMDF 客户端驱动程序，在其[ **WdfUsbInterfaceSelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)调用，该驱动程序可以提供指向驱动程序定义管道上下文的指针。 客户端驱动程序可以在管道上下文中存储有关管道的信息。 有关管道的信息的详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

## <a name="related-topics"></a>相关主题
[USB 设备配置](configuring-usb-devices.md)  



