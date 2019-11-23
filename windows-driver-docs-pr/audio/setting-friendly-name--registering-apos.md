---
title: 设置友好名称，注册 APO
description: 本主题介绍 Port 类蓝牙 sideband audio 驱动程序如何设置设备接口的友好名称，以及如何注册蓝牙设备使用的任何 APO。
ms.assetid: A3C4E04C-8F3B-49B4-8E46-CF37E1A4F5AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5df16c68791aab1470f906f25a3b0565fdc01dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830126"
---
# <a name="setting-friendly-names-registering-apos"></a>设置友好名称，注册 APO


设置友好名称（注册）主题介绍 Port 类蓝牙 sideband audio 驱动程序如何为设备接口设置友好名称，以及注册蓝牙设备使用的任何音频处理对象（APO）。

对于每个已启用的 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口，端口类音频驱动程序（PortCls）通常会调用 PcRegisterSubdevice 函数，该函数在音频适配器上注册代表子设备的 PnP 设备接口。 在典型的音频驱动程序设计中，音频驱动程序对 "wave" 和 "拓扑" 子设备调用 PcRegisterSubdevice，然后通过调用其他端口类函数连接。

在为 "拓扑" 子设备调用 PcRegisterSubdevice 之前，驱动程序按照[设置属性和注册表值](setting-properties-and-registry-values.md)中所述的过程，在 KSCATEGORY\_音频接口类的接口上设置属性和注册表值。 以下各节介绍了具体的属性和注册表值。

## <a name="span-iddevpkey_deviceinterface_friendlynamespanspan-iddevpkey_deviceinterface_friendlynamespanspan-iddevpkey_deviceinterface_friendlynamespandevpkey_deviceinterface_friendlyname"></a><span id="DEVPKEY_DeviceInterface_FriendlyName"></span><span id="devpkey_deviceinterface_friendlyname"></span><span id="DEVPKEY_DEVICEINTERFACE_FRIENDLYNAME"></span>DEVPKEY\_DeviceInterface\_FriendlyName


音频驱动程序将[ **\_BTHHFP\_设备发送 IOCTL，\_获取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)对免提配置文件（HFP）音频驱动程序的\_描述符请求。 请求的信息以[**BTHHFP\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)结构的形式返回，以及结构引用的其他数据。 然后，音频驱动程序调用 IoSetDeviceInterfacePropertyData，将 DEVPKEY\_DeviceInterface\_FriendlyName 设置为**BTHHFP\_描述符**结构的*FriendlyName*字段中的值。

音频驱动程序将参数设置为 IoSetDeviceInterfacePropertyData，如下所示：

-   SymbolicLinkName = 从 IoRegisterDeviceInterface 返回的字符串

-   PropertyKey = DEVPKEY\_DeviceInterface\_FriendlyName

-   Lcid = 区域设置\_中立

-   Flags = PLUGPLAY\_属性\_永久性

-   Type = DEVPROP\_类型\_字符串\_间接

-   Size = BTHHFP\_描述符。FriendlyName. Length + sizeof （UNICODE\_NULL）

-   Data = BTHHFP\_描述符。FriendlyName. Buffer

## <a name="span-idapo_registrationspanspan-idapo_registrationspanspan-idapo_registrationspanapo-registration"></a><span id="APO_registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 注册


如[设置属性和注册表值](setting-properties-and-registry-values.md)中所述，驱动程序可以设置设备接口的注册表值。 若要注册 APO，音频驱动程序会在设备接口上设置多个值。 这些值与通常在 INF 中为 APO 注册设置的值相同，特定值将从一个音频驱动程序更改为下一个。

下面是用于注册 APO 的 INF 文件语法示例：

``` syntax
HKR,"EPFX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"EPFX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
```

**请注意**  前面代码段中所示的语法不包含用于注册 APO 的 COM 服务器的说明。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[相关设计准则](related-design-guidelines.md)  



