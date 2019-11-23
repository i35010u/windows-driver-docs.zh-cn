---
Description: 本主题介绍发出选择接口请求以激活 USB 接口中的替代设置的步骤。
title: 如何在 USB 界面中选择备用设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d82ce7f0d7c988fc84c9e1f82f72005d82c4e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824185"
---
# <a name="how-to-select-an-alternate-setting-in-a-usb-interface"></a>如何在 USB 界面中选择备用设置


本主题介绍发出选择接口请求以激活 USB 接口中的替代设置的步骤。 在选择 USB 配置之后，客户端驱动程序必须发出此请求。 默认情况下，选择配置还会激活该配置的每个接口中的第一个备用设置。

每个 USB 配置必须支持一个或多个 USB 接口。 每个接口都公开一个或多个用于在设备之间传输数据的终结点。 USB 接口必须具有用于标识接口的设备定义的*接口索引*。 接口还必须具有一个或多个对接口的终结点进行分组的*备用设置*。 在设备配置过程中，客户端驱动程序必须在接口中选择一个备用设置。 由于终结点可以在备用设置之间共享，因此在给定时间只能有一个设置处于活动状态。 备用设置处于活动状态后，其终结点就可用于数据传输。

对于多接口设备，可在给定时间激活两个接口。 客户端驱动程序必须激活每个接口中的备用设置。 终结点不会在接口之间共享，因此，每个同步数据传输可以在每个接口上执行。

备用设置由设备定义，并使用一个称为*设置索引*的数字标识。 索引0处的备用设置称为此文档集中的*默认备用设置*。 [**USB\_接口\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)结构中介绍了替代设置。 结构包含与设置关联的接口索引以及设置定义的终结点的数目。 它还包含有关接口功能所遵守的类规范的信息。 对终结点进行分组的方式取决于设备的功能。

例如，接口通过三个替代设置（索引0、1、2）公开两个按下的和两个大容量终结点。 备用设置0未定义任何终结点;替换设置1定义大容量终结点;备用设置2定义同步终结点。 由于备用设置0没有终结点，因此客户端驱动程序可以选择此设置来禁用数据传输，以便节省带宽。 如果任何一个设置处于活动状态，则设备可以进行数据传输。 备用设置1可用于传输大容量数据。 当设备处于流模式时，可以选择 "备用设置 2"。 因此，备用设置为客户端驱动程序提供了根据需要更改设备配置的灵活性。 在此示例中，客户端驱动程序可以将设备功能从大容量传输转换为流式传输，只需选择备用设置即可。

备用设置也可用于设置带宽要求。 有关示例，请参阅[USB 设备布局](usb-device-layout.md)。

Windows Driver Foundation （WDF）提供[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)和[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)中的方法，客户端驱动程序可调用该框架来选择其他替代设置。 KMDF 客户端驱动程序可以通过指定设置索引、设置的接口描述符或提交包含请求的 URB 来选择设置。 UMDF 客户端驱动程序只能通过指定其设置索引来选择替代设置。

在选择配置请求成功完成后，将停用先前活动的备用设置。

## <a name="what-you-need-to-know"></a>你需要了解的内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>必备条件

在客户端驱动程序可以选择备用设置之前，请确保满足以下要求：

-   客户端驱动程序必须已创建框架 USB 目标设备对象。

    -   KMDF 客户端驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法来获取 WDFUSBDEVICE 句柄。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md) 中的“设备源代码”。
    -   UMDF 客户端驱动程序必须通过查询框架目标设备对象获取 [**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) 指针。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构（UMDF）](understanding-the-umdf-template-code-for-usb.md)中的 "[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)实现和特定于 USB 的任务"

    如果使用的是随 Microsoft Visual Studio Professional 2012 一起提供的 USB 模板，则模板代码将执行这些任务。 模板代码会获取目标设备对象的句柄并将其存储在设备上下文中。

-   设备必须具有活动配置。
    -   KMDF 客户端驱动程序必须调用[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)方法。
    -   对于 UMDF 客户端驱动程序，框架为该配置中的每个接口选择第一个配置和默认备用设置。

    如果使用的是 USB 模板，则代码将选择每个接口中的第一个配置和默认备用设置。

<a name="instructions"></a>说明
------------

### <a name="select-an-alternate-setting---kmdf-client-driver"></a>选择替代设置-KMDF 客户端驱动程序

1.  获取具有替代设置的接口的 WDFUSBINTERFACE 句柄。

    若要获取句柄，请先通过调用[**WdfUsbTargetDeviceGetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetnuminterfaces)并在循环中枚举接口，来获取所选配置的接口数。 在每次迭代中调用[**WdfUsbTargetDeviceGetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)方法，并递增索引（从零开始）。

    **注意**  设备枚举过程中，USB 驱动程序堆栈会将编号分配给备用设置。 接口编号从零开始，并按顺序排列。 这些数字可能不同于设备定义的设置索引。 若要获取设备定义的设置索引，请调用[**WdfUsbInterfaceGetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetinterfacenumber)方法。

     

2.  通过调用[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)方法启动一个选择接口请求。 在调用的*Params*参数中，选择以下选项之一：

    -   指定 USB 驱动程序堆栈分配的备用设置编号。 通常，传递在步骤1中使用的同一索引来枚举设置。
    -   指定一个指针，该指针是描述替代设置的接口描述符。 然后，该驱动程序可以通过调用[**WdfUsbInterfaceGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)方法来在接口中枚举替代设置时获取接口描述符。 枚举完成后，驱动程序将获取有关[**USB\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)中所有枚举的替代设置的信息\_描述符结构。
    -   指定指向 URB 的指针，该指针包含选择接口请求所需的所有信息。

        1.  将[**USBD\_接口的数组分配\_列表\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)结构。 此数组中的元素数取决于所选配置中的接口数。 有关初始化此阵列的信息，请参阅[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。
        2.  通过调用[**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)例程，为 select 接口请求分配一个[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 。 在此调用中指定接口列表数组和在选择配置后获取的配置句柄。 可以通过调用[**WdfUsbTargetDeviceWdmGetConfigurationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicewdmgetconfigurationhandle)方法获取该句柄。
        3.  调用[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)并指定 URB。

        **WDM 驱动程序：  **若要提交 URB，请将 URB 与 IRP 关联，并将 IRP 提交到 USB 驱动程序堆栈。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

    列表中的选项为客户端驱动程序提供了指定选择条件的灵活性。 如果已了解备用设置的终结点功能，请在列表中选择第一个选项（带有备用设置编号）。 否则，请选择第二个选项来指定接口描述符。 检查[**USB\_接口\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)所有替换设置的描述符结构。 对于每个设置，枚举其终结点及其特性，如终结点类型、最大数据包大小等。 如果找到了数据传输所需的终结点集，请通过指定指向该接口描述符的指针来调用[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting) 。 通常，您不需要第三个选项，除非您是基于 WDM 的客户端驱动程序，该驱动程序只能通过提交 URBs 将请求发送到 USB 驱动程序堆栈。

    根据客户端驱动程序提供的信息，USB 驱动程序堆栈会构建标准控制请求（设置接口），并将其发送到设备。 如果请求成功完成，则 USB 驱动程序堆栈会将管道句柄获取到备用设置的终结点。

    选择备用设置后，客户端驱动程序必须始终获取新设置中的终结点的管道句柄。 否则，可能会导致驱动程序通过使用陈旧的管道句柄发送数据传输请求。 有关检索管道句柄的信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

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

### <a name="select-an-alternate-setting---umdf-client-driver"></a>选择备用设置-UMDF 客户端驱动程序

1.  调用[**IWDFUsbTargetDevice：： GetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)方法获取活动配置支持的 USB 接口数。
2.  获取配置中每个接口的[**IWDFUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)指针。

    通过在循环中调用[**IWDFUsbTargetDevice：： RetrieveUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)方法来枚举所有接口，直到该函数返回 NULL。 对于每个迭代，递增成员索引（从零开始）。 循环检索指向所有枚举接口的[**IWDFUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)指针。

3.  对于每个接口，请通过调用[**IWDFUsbInterface：： GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)获取 WinUSB 句柄。 下一步需要此句柄。
4.  调用[**WinUsb\_GetAssociatedInterface**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface)获取接口的句柄。 在*AssociatedInterfaceIndex*参数中，在步骤2中指定索引。
5.  确定接口中的替代设置的数目。

    在循环中调用[**WinUsb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)函数，并在每次迭代中递增索引（从零开始）。 枚举所有设置后，函数将返回错误，\_不\_多个\_项。 函数还返回每个设置的接口描述符。

6.  通过使用每个接口描述符的**bNumEndpoints**成员中接收的值并枚举其终结点。 检查终结点描述符，确定哪个设置满足你的要求。
7.  通过调用[**WinUsb\_SetCurrentAlternateSetting**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting)函数来启动选择接口请求。 在调用中，指定与步骤4中的索引关联的备用设置号。
8.  通过调用[**WinUsb\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)函数，释放在步骤4中获取的接口句柄。
9.  通过调用[**WinUSB\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)函数，释放在步骤3中获取的 WinUSB 句柄。
10. 如果使用完[**IWDFUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)方法，请释放在步骤2中检索到的所有接口指针。

<a name="remarks"></a>备注
-------

对于 KMDF 客户端驱动程序，在其[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)调用中，驱动程序可以提供指向驱动程序定义的管道上下文的指针。 客户端驱动程序可以将有关管道的信息存储在管道上下文中。 有关管道信息的详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

## <a name="related-topics"></a>相关主题
[USB 设备配置](configuring-usb-devices.md)  



