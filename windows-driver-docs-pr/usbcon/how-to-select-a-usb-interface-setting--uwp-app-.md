---
description: 使用 UsbInterfaceSetting 对象获取当前设置并在接口中设置设置。
title: 如何选择 USB 接口设置（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 172de8b6fa664d78a3d080da9840068d91ac0c38
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009945"
---
# <a name="how-to-select-a-usb-interface-setting-uwp-app"></a>如何选择 USB 接口设置（UWP 应用）

本主题介绍如何更改 USB 接口内的设置。 你将使用 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting) 对象获取当前设置并在接口中设置设置。

## <a name="before-you-start"></a>准备工作

- 必须已打开设备并获得 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象。 阅读 [如何)  (UWP 应用连接到 USB 设备 ](how-to-connect-to-a-usb-device--uwp-app-.md)。
- 代码示例基于 CustomUSBDevice 示例。 您可以从此代码库页下载完整的示例。

## <a name="about-usb-interface-settings"></a>关于 USB 接口设置

每个 USB 接口都公开一个或多个按 *接口设置*分组的终结点。 这些设置由设备定义，并由一个称为 *设置索引*的数字标识。 每个接口必须 *只有一个* 活动的设置。 对于多接口设备，每个接口都必须有一个活动的设置。 如果设置处于活动状态，则可以将数据传输到其终结点或从其终结点传输数据。 对于数据传输，禁用非活动设置中的终结点。

在设备上选择设置后，将其视为处于活动状态。 默认活动设置是接口的第一个设置。

每个设置都由一个 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting) 对象表示。 通过使用对象，UWP 应用可以执行以下操作：

- 确定在枚举接口中的所有设置时特定设置是否处于活动状态。
- 启动一个选择设置的请求。

有关 USB 接口设置的信息，请参阅 [usb 设备布局](usb-device-layout.md)。

## <a name="get-the-active-setting-of-a-usb-interface"></a>获取 USB 接口的活动设置

1. 从上一个获取的[**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice)对象获取[**UsbInterface**](/uwp/api/Windows.Devices.Usb.UsbInterface)对象。 此代码示例获取 USB 配置中的第一个接口。 对于多接口设备，可以通过枚举所有接口获取要使用的 **UsbInterface** 对象。 可以通过 [**UsbConfiguration. UsbInterfaces**](/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_UsbInterfaces) 属性值获取该数组。
2. 通过获取[**UsbInterface. InterfaceSettings**](/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_InterfaceSettings)属性值，获取接口中定义为[**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)对象数组的所有设置。
3. 枚举数组，并在每次迭代中检查该设置是否处于活动状态，方法是检查 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Selected) 属性。

此示例代码演示如何获取默认接口中定义的所有设置的设置号。

```CSharp
void GetInterfaceSetting (UsbDevice device)
{
        auto interfaceSettings = device.InterfaceSettings;

        for each(UsbInterfaceSetting interfaceSetting in interfaceSettings)
        {
            if (interfaceSetting->Selected)
            {
                uint8 interfaceSettingNumber = interfaceSetting.InterfaceDescriptor.AlternateSettingNumber;

                // Use the interface setting number. Not shown.

                break;
            }
        }
}
```

## <a name="set-a-usb-interface-setting"></a>设置 USB 接口设置

若要选择当前处于非活动状态的设置，必须找到 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting) 对象，以便选择该设置，然后通过调用 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync) 方法启动异步操作。 此操作不返回值。

```CSharp
private async void SetInterfaceSetting(UsbDevice device, Byte settingNumber)
{
    var interfaceSetting = device.DefaultInterface.InterfaceSettings[settingNumber];

    await interfaceSetting.SelectSettingAsync();

    MainPage.Current.NotifyUser("Interface Setting is set to " + settingNumber, NotifyType.StatusMessage);
}
```

## <a name="see-also"></a>另请参阅

[**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Selected)

[**UsbInterfaceSetting.SelectSettingAsync**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync)