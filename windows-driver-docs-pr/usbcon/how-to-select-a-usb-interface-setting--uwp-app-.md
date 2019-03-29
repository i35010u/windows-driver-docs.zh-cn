---
Description: 使用 UsbInterfaceSetting 对象获取的当前设置和界面中设置的设置。
title: 如何选择 USB 接口设置（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03fb325f51542bb3b6441ecc9170db3f79d6d74a
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419561"
---
# <a name="how-to-select-a-usb-interface-setting-uwp-app"></a>如何选择 USB 接口设置（UWP 应用）

本主题介绍有关更改 USB 接口内的设置。 将使用[ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)对象来获取当前设置，并在界面中设置的设置。

## <a name="before-you-start"></a>开始之前

- 您必须打开设备并获取[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象。 读取[如何连接到 USB 设备 （UWP 应用）](how-to-connect-to-a-usb-device--uwp-app-.md)。
- 代码示例基于 CustomUSBDevice 示例。 您可以从该页的代码库下载完整的示例。

## <a name="about-usb-interface-settings"></a>有关 USB 接口设置

每个 USB 接口公开一个或多个终结点，中的分组*界面设置*。 这些设置是设备定义，使用一个称为的数字标识*设置索引*。 每个接口必须有*只有一个*活动设置。 对于多个接口设备，每个接口都必须具有活动的设置。 如果设置为活动，数据可以传输到或从其终结点。 对于数据传输已禁用非活动设置中的终结点。

一种设置称为后已选择在设备上处于活动状态。 默认活动设置为第一个接口的设置。

每个设置为由[ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)对象。 通过使用对象，UWP 应用可以执行这些操作：

- 确定某个特定的设置枚举的接口中的所有设置时是否处于活动状态。
- 启动选择一项设置的请求。

有关 USB 接口设置的信息，请参阅[USB 设备布局](usb-device-layout.md)。

## <a name="get-the-active-setting-of-a-usb-interface"></a>获取活动的 USB 接口设置

1. 获取[ **UsbInterface** ](https://msdn.microsoft.com/library/windows/apps/dn264121)之前获取的对象[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象。 此代码示例将获取 USB 配置中的第一个接口。 对于多个接口设备，可以获取**UsbInterface**对象想要使用通过枚举所有接口。 可以通过获取该数组[ **UsbConfiguration.UsbInterfaces** ](https://msdn.microsoft.com/library/windows/apps/dn263808)属性值。
2. 获取数组的形式在接口中定义的所有设置[ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)对象通过获取[ **UsbInterface.InterfaceSettings** ](https://msdn.microsoft.com/library/windows/apps/dn264291)属性值。
3. 枚举数组和每次迭代中检查设置是否通过检查 active [ **UsbInterfaceSetting.Selected** ](https://msdn.microsoft.com/library/windows/apps/dn264285)属性。

此示例代码演示如何获取设置数字的默认接口中定义的所有设置。

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

## <a name="set-a-usb-interface-setting"></a>将 USB 接口设置

若要选择不是当前处于活动状态的设置，你必须发现[ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)对象选择，然后通过调用开始异步操作，设置[ **UsbInterfaceSetting.SelectSettingAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264286)方法。 该操作不返回值。

```CSharp
private async void SetInterfaceSetting(UsbDevice device, Byte settingNumber)
{
    var interfaceSetting = device.DefaultInterface.InterfaceSettings[settingNumber];

    await interfaceSetting.SelectSettingAsync();

    MainPage.Current.NotifyUser("Interface Setting is set to " + settingNumber, NotifyType.StatusMessage);
}
```

# <a name="see-also"></a>请参阅

[**UsbInterfaceSetting.Selected**](https://msdn.microsoft.com/library/windows/apps/dn264285)

[**UsbInterfaceSetting.SelectSettingAsync**](https://msdn.microsoft.com/library/windows/apps/dn264286)
