---
Description: 本主题提供了有关注册表设置的信息，这些设置用于配置 Usbccgp 选择 USB 配置的方式。
title: 配置 Usbccgp.sys，选择非默认 USB 配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2bf07d32a6e04baa14eadab2c365ca65ab6927
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824184"
---
# <a name="configuring-usbccgpsys-to-select-a-non-default-usb-configuration"></a>配置 Usbccgp.sys，选择非默认 USB 配置


本主题提供了有关注册表设置的信息，这些设置用于配置 Usbccgp 选择 USB 配置的方式。 本主题还介绍了 Usbccgp 如何处理由客户端驱动程序发送的用于控制复合设备功能的客户端驱动程序的选择配置请求。




USB 复合设备包含一个 USB 设备内的多个功能（功能设备）。 如果 Windows 为复合设备加载 Microsoft 提供的[USB 通用父驱动程序](usb-common-class-generic-parent-driver.md)（Usbccgp），则从该点开始，Usbccgp 负责选择设备的配置。 复合设备的每个接口或接口集合在很多方面都是指具有自己的物理设备对象（PDO）的单独设备。 重置设备的配置将更改所有设备接口的配置，而不只是客户端驱动程序控制的接口。 操作系统不允许这样做。 因此，控制一组接口或复合设备的接口集合的客户端驱动程序不能更改最初由 Usbccgp 设置的配置。

但是，在 Windows Vista 和更高版本的 Windows 中，你可以添加以下注册表值，以指定要选择的配置：

| 注册表项               | 在任务栏的搜索框中键入       | 值                                                                                                          | Default Value |
|----------------------------|------------|----------------------------------------------------------------------------------------------------------------|---------------|
| OriginalConfigurationValue | REG\_DWORD | USB 配置索引。 Usbccgp 对选择配置请求使用 OriginalConfigurationValue。 | 0             |
| AltConfigurationValue      | REG\_DWORD | 在 OriginalConfigurationValue 的选择配置请求失败时要使用的配置索引。      | 0             |

 

**请注意**，默认情况下  前面的注册表设置不存在。 它们必须添加到 USB 设备的[硬件（也称为 "设备"）密钥](https://docs.microsoft.com/windows-hardware/drivers/install/opening-a-device-s-hardware-key)下。

 

注册表设置允许 CCGP 驱动程序选择其他配置。

上表中描述的注册表值对应于 USB 定义的配置索引，由配置描述符（[**USB\_配置\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)）的**bConfigurationValue**成员指示，而*不*是由设备配置描述符中报告的**bConfigurationNum**值指示。 首先，Usbccgp 使用 OriginalConfigurationValue 指定的 USB 配置索引将选择配置请求发送到父 USB 总线驱动程序（Usbhub）。 如果该请求失败，Usbccgp 将尝试使用 AlternateConfigurationValue 中指定的值。 如果 AlternateConfigurationValue 或 OriginalConfigurationValue 无效，Usbccgp 将使用默认值。

由于许多原因，选择配置请求可能会失败。 如果设备未正确响应请求或**bMaxPower**值（请求的配置所需的电源）超过集线器端口支持的功率值，则会出现最常见的故障。 例如，特定配置的**bMaxPower** （由 OriginalConfigurationValue 指定）为 100 milliamperes，但集线器端口只能提供 50 milliamperes。 当 Usbccgp 发送对该配置的选择配置请求时，USB 驱动程序堆栈（具体而言，是 USB 端口驱动程序）将无法请求。 然后，Usbccgp 通过指定 AltConfigurationValue 指示的配置发送另一个选择配置请求。 如果备用配置要求 50 milliamperes 或更少，且未出现其他问题，则选择-配置请求会成功完成。

### <a href="" id="compatibility-feature"></a>兼容性功能

即使复合设备中某个函数的客户端驱动程序无法选择复合设备的配置，客户端驱动程序仍可以向 Usbccgp 发送选择-配置请求。 有关如何生成该请求的信息，请参阅[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。 Usbccgp 在接收来自客户端驱动程序的选择配置请求后执行以下任务：

1.  使用 USB 端口驱动程序用于验证任何选择配置请求的相同条件来验证收到的请求。
2.  如果请求指定了不同于当前设置的接口或管道设置，Usbccgp 将通过发送 URB\_函数类型的 URB 发出一个选择接口请求\_选择\_接口以将现有设置更改为新的接口和管道设置。
3.  将[**USBD\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information)的缓存内容复制到 URB 中\_信息和[**USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构。
4.  完成 URB。

## <a name="related-topics"></a>相关主题
[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)  
[USB 设备配置](configuring-usb-devices.md)  



