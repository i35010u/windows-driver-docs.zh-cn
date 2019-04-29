---
Description: 本主题提供 Usbccgp.sys 选择 USB 配置注册表设置配置的方式的信息。
title: 配置 Usbccgp.sys，选择非默认 USB 配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45009bca190ff1fc97611511e6282af18781436a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379511"
---
# <a name="configuring-usbccgpsys-to-select-a-non-default-usb-configuration"></a>配置 Usbccgp.sys，选择非默认 USB 配置


本主题提供 Usbccgp.sys 选择 USB 配置注册表设置配置的方式的信息。 本主题还介绍如何 Usbccgp.sys 处理发送的控制功能的复合设备之一的客户端驱动程序选择配置请求。




USB 复合设备包含的单个 USB 设备中的多个函数 （功能的设备）。 如果 Windows 加载由 Microsoft 提供[USB 通用父驱动程序](usb-common-class-generic-parent-driver.md)(Usbccgp.sys) 对于复合设备，从该时间点，Usbccgp.sys 负责选择设备的配置。 每个接口或复合设备的接口集合是，在许多方面，如具有其自己的物理设备的对象 (PDO) 的单独设备。 重置设备的配置更改的所有设备的接口，而不仅仅是一个客户端驱动程序控制的配置。 操作系统不允许这样。 因此，控制一组接口或接口集合的复合设备的客户端驱动程序不能更改最初通过 Usbccgp.sys 设置的配置。

但是，在 Windows Vista 和更高版本的 Windows 中，可以添加以下注册表值，以指定要选择的配置：

| 注册表项               | 在任务栏的搜索框中键入       | ReplTest1                                                                                                          | 默认值 |
|----------------------------|------------|----------------------------------------------------------------------------------------------------------------|---------------|
| OriginalConfigurationValue | REG\_DWORD | USB 配置索引。 Usbccgp.sys 使用 OriginalConfigurationValue 首先选择配置请求。 | 0             |
| AltConfigurationValue      | REG\_DWORD | 要与 OriginalConfigurationValue 选择配置请求失败时使用的配置索引。      | 0             |

 

**请注意**  前面的注册表设置不存在，默认情况下。 必须将它们添加下[硬件 （也称为"设备"） 密钥](https://docs.microsoft.com/windows-hardware/drivers/install/opening-a-device-s-hardware-key)的 USB 设备。

 

注册表设置允许 CCGP 驱动程序，以选择备用的配置。

前面的表中所述的注册表值对应于指示的 USB 定义的配置索引**bConfigurationValue**配置描述符的成员 ([**USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)) 和*不*通过**bConfigurationNum**报告设备的配置中的值描述符。 首先，Usbccgp.sys 选择配置向发送请求父 USB 总线驱动程序 (Usbhub.sys) 通过使用指定 OriginalConfigurationValue 的 USB 配置索引。 如果该请求失败，Usbccgp.sys 将尝试使用 AlternateConfigurationValue 中指定的值。 Usbccgp.sys 如果 AlternateConfigurationValue 或 OriginalConfigurationValue 无效，则使用默认值。

原因有很多情况下，选择配置请求可能会失败。 或设备未正确响应请求时，将发生最常见故障**bMaxPower**值 （由所请求的配置所需的电源） 超出了支持中心端口的电源值。 例如， **bMaxPower** （由 OriginalConfigurationValue 指定） 的特定配置是 100 毫安但中心端口才能够提供 50 毫安。 当 Usbccgp.sys 发送选择配置请求为该配置时，USB 驱动程序堆栈 （具体而言，USB 端口驱动程序） 将使请求失败。 Usbccgp.sys 然后通过指定配置为由 AltConfigurationValue 发送另一个选择配置请求。 如果备用配置需要 50 毫安或更少的和任何其他问题发生，选择配置请求已成功完成。

### <a href="" id="compatibility-feature"></a> 兼容性功能

即使复合设备中的函数的客户端驱动程序不能选择复合设备的配置，客户端驱动程序仍可以向 Usbccgp.sys 发送选择配置请求。 有关如何生成该请求的信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。 Usbccgp.sys 收到来自客户端驱动程序的选择配置请求后执行以下任务：

1.  通过使用 USB 端口驱动程序用来验证任何选择配置请求的条件相同验证收到的请求。
2.  如果该请求指定了不同于当前设置的接口或管道设置，Usbccgp.sys 发出选择接口请求通过发送类型 URB URB\_函数\_选择\_接口更改新的接口和管道设置到现有的设置。
3.  将复制的缓存的内容[ **USBD\_界面\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539068)并[ **USBD\_管道\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539114)到 URB 的结构。
4.  完成 URB。

## <a name="related-topics"></a>相关主题
[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)  
[USB 设备配置](configuring-usb-devices.md)  



