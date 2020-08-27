---
description: 本主题提供有关配置 Usbccgp.sys 选择 USB 配置方式的注册表设置的信息。
title: 配置 Usbccgp.sys，选择非默认 USB 配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 444283b274c79a4387f925e0c092ddafbd1742d5
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969468"
---
# <a name="configuring-usbccgpsys-to-select-a-non-default-usb-configuration"></a>配置 Usbccgp.sys，选择非默认 USB 配置


本主题提供有关配置 Usbccgp.sys 选择 USB 配置方式的注册表设置的信息。 本主题还介绍 Usbccgp.sys 如何处理客户端驱动程序发送的控制复合设备功能之一的选择配置请求。




USB 复合设备由多个功能组成， (功能设备在单个 USB 设备中) 。 如果 Windows 加载 Microsoft 提供的 [USB 通用父驱动程序](usb-common-class-generic-parent-driver.md) ( # A0) 对于复合设备，则从该点开始，Usbccgp.sys 负责选择设备的配置。 复合设备的每个接口或接口集合在很多方面都是类似于具有其自己的物理设备对象 (PDO) 的单独设备。 重置设备的配置将更改所有设备接口的配置，而不只是客户端驱动程序控制的接口。 操作系统不允许这样做。 因此，控制一组接口或复合设备的接口集合的客户端驱动程序不能更改最初由 Usbccgp.sys 设置的配置。

但是，在 Windows Vista 和更高版本的 Windows 中，你可以添加以下注册表值，以指定要选择的配置：

| 注册表项               | 类型       | 值                                                                                                          | 默认值 |
|----------------------------|------------|----------------------------------------------------------------------------------------------------------------|---------------|
| OriginalConfigurationValue | REG \_ DWORD | USB 配置索引。 Usbccgp.sys 首先将 OriginalConfigurationValue 用于选择配置请求。 | 0             |
| AltConfigurationValue      | REG \_ DWORD | 在 OriginalConfigurationValue 的选择配置请求失败时要使用的配置索引。      | 0             |

 

**注意**   默认情况下，前面的注册表设置不存在。 必须在硬件下添加这些设备， (称为 USB 设备的 ["设备" ) 密钥](https://docs.microsoft.com/windows-hardware/drivers/install/opening-a-device-s-hardware-key) 。

 

注册表设置允许 CCGP 驱动程序选择其他配置。

上表中描述的注册表值对应于 USB 定义的配置索引，由配置描述符的 **bConfigurationValue** 成员指示 ([**usb \_ 配置 \_ 描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)) ，而 *不* 是由设备配置描述符中报告的 **bConfigurationNum** 值指示。 首先，Usbccgp.sys 使用 OriginalConfigurationValue 指定的 USB 配置索引向父 USB 总线驱动程序 ( # A1) 发送选择配置请求。 如果该请求失败，Usbccgp.sys 将尝试使用 AlternateConfigurationValue 中指定的值。 如果 AlternateConfigurationValue 或 OriginalConfigurationValue 无效，Usbccgp.sys 使用默认值。

由于许多原因，选择配置请求可能会失败。 如果设备未正确响应请求，或者请求的) 配置所需的 **bMaxPower** 值 (功率超出集线器端口支持的功率值，则会出现最常见的故障。 例如，OriginalConfigurationValue) 指定 (的特定配置的 **bMaxPower** 为 100 milliamperes，但集线器端口只能提供 50 milliamperes。 当 Usbccgp.sys 发送该配置的选择配置请求时，USB 驱动程序堆栈 (具体而言，usb 端口驱动程序) 请求失败。 然后 Usbccgp.sys 通过指定 AltConfigurationValue 指示的配置发送另一个选择配置请求。 如果备用配置要求 50 milliamperes 或更少，且未出现其他问题，则选择-配置请求会成功完成。

### <a name="compatibility-feature"></a><a href="" id="compatibility-feature"></a> 兼容性功能

即使复合设备中某个函数的客户端驱动程序无法选择复合设备的配置，客户端驱动程序仍可将选择配置请求发送到 Usbccgp.sys。 有关如何生成该请求的信息，请参阅 [如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。 Usbccgp.sys 在接收来自客户端驱动程序的选择配置请求后执行以下任务：

1.  使用 USB 端口驱动程序用于验证任何选择配置请求的相同条件来验证收到的请求。
2.  如果请求指定了不同于当前设置的接口或管道设置，则 Usbccgp.sys 通过发送类型 URB 函数 select 接口的 URB 发出 select-interface 请求， \_ \_ \_ 以将现有设置更改为新的接口和管道设置。
3.  将 [**USBD \_ 接口 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_interface_information) 和 [**USBD \_ 管道 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information) 结构的缓存内容复制到 URB 中。
4.  完成 URB。

## <a name="related-topics"></a>相关主题
[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)  
[USB 设备配置](configuring-usb-devices.md)  



