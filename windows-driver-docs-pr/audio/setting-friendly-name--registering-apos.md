---
title: 设置友好名称，注册 APO
description: 本主题介绍如何设置设备接口的友好名称和注册的蓝牙设备使用任何 APO 端口类蓝牙旁带音频驱动程序。
ms.assetid: A3C4E04C-8F3B-49B4-8E46-CF37E1A4F5AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1aa3cb6200531ecb98936cf13510e23bebe341c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355253"
---
# <a name="setting-friendly-names-registering-apos"></a>设置友好名称，注册 APO


设置友好名称，注册 a p o s 主题介绍如何设置设备接口的友好名称和注册的蓝牙设备使用的任何音频处理对象 (APO) 端口类蓝牙旁带音频驱动程序。

对于每个启用了 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口，音频驱动程序 (PortCls) 通常调用 PcRegisterSubdevice 函数时，将其注册端口类表示子音频适配器上的设备的即插即用设备接口。 在典型的音频驱动程序设计中，音频驱动程序"波形"和"拓扑"子设备，然后通过调用其他端口类函数连接调用 PcRegisterSubdevice。

在调用之前 PcRegisterSubdevice"拓扑"子设备，该驱动程序都遵循的过程中所述[设置属性和注册表值](setting-properties-and-registry-values.md)KSCATEGORY中的接口上设置属性和注册表值\_音频接口类。 以下各节所述的特定属性值和注册表值。

## <a name="span-iddevpkeydeviceinterfacefriendlynamespanspan-iddevpkeydeviceinterfacefriendlynamespanspan-iddevpkeydeviceinterfacefriendlynamespandevpkeydeviceinterfacefriendlyname"></a><span id="DEVPKEY_DeviceInterface_FriendlyName"></span><span id="devpkey_deviceinterface_friendlyname"></span><span id="DEVPKEY_DEVICEINTERFACE_FRIENDLYNAME"></span>DEVPKEY\_DeviceInterface\_FriendlyName


音频驱动程序发送[ **IOCTL\_BTHHFP\_设备\_获取\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)无配置文件 (HFP) 音频驱动程序的请求。 中的形式返回请求的信息[ **BTHHFP\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)结构，以及其他数据，引用的结构。 音频驱动程序，然后调用 IoSetDeviceInterfacePropertyData 设置 DEVPKEY\_DeviceInterface\_中的值的 FriendlyName *FriendlyName*字段**BTHHFP\_描述符**结构。

音频驱动程序设置的参数 IoSetDeviceInterfacePropertyData，如下所示：

-   SymbolicLinkName = IoRegisterDeviceInterface 从返回的字符串

-   PropertyKey = DEVPKEY\_DeviceInterface\_FriendlyName

-   Lcid = 区域设置\_非特定语言

-   标志 = PLUGPLAY\_属性\_的永久

-   类型 = DEVPROP\_类型\_字符串\_间接

-   Size = BTHHFP\_DESCRIPTOR.FriendlyName.Length + sizeof(UNICODE\_NULL)

-   Data = BTHHFP\_DESCRIPTOR.FriendlyName.Buffer

## <a name="span-idaporegistrationspanspan-idaporegistrationspanspan-idaporegistrationspanapo-registration"></a><span id="APO_registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 注册


如中所述[设置属性和注册表值](setting-properties-and-registry-values.md)，驱动程序可以设置设备接口的注册表值。 若要注册 APO，音频驱动程序，请设置设备接口上的多个值。 这些值是不同于通常为 APO 注册 INF 中设置和特定的值将从一个音频驱动程序更改为下一步。

下面是用于注册 APO 的 INF 文件语法的示例：

``` syntax
HKR,"EPFX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"EPFX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
```

**请注意**  前面代码片段所示的语法不包含有关注册 APO 的 COM 服务器的说明。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[相关的设计准则](related-design-guidelines.md)  



