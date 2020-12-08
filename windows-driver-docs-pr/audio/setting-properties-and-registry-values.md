---
title: 设置属性和注册表值
description: 设置属性和注册表值主题介绍了 Port 类音频驱动程序如何设置 PnP 设备接口的属性和注册表值。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88b4a2a19f65785d8af6e2029f00352f1b5bd526
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800669"
---
# <a name="setting-properties-and-registry-values"></a>设置属性和注册表值


设置属性和注册表值主题介绍了 Port 类音频驱动程序如何设置 PnP 设备接口的属性和注册表值。

端口类音频驱动程序 Portcls 必须执行以下步骤以正确注册设备接口并设置所需的值。

## <a name="span-id1_register_the_device_interfacespanspan-id1_register_the_device_interfacespan1-register-the-device-interface"></a><span id="1._register_the_device_interface"></span><span id="1._REGISTER_THE_DEVICE_INTERFACE"></span>1. 注册设备接口


在为子设备调用 PcRegisterSubdevice 之前，驱动程序可以直接调用 IoRegisterDeviceInterface 来注册 KSCATEGORY \_ 音频接口。 这样，驱动程序便有机会在设备接口上设置接口属性和注册表值，然后 PcRegisterSubdevice 注册和启用接口。

音频驱动程序设置 IoRegisterDeviceInterface 的参数，如下所示。

-   PhysicalDeviceObject 参数是 \_ 音频驱动程序可从 PcGetPhysicalDeviceObject 函数检索的 PDEVICE 对象。

-   InterfaceClassGuid 设置为接口的类 GUID。

-   ReferenceString 与音频驱动程序传递给 PcRegisterSubdevice 的 Name 参数相同。

成功完成上述任务后，IoRegisterDeviceInterface 将返回已注册接口的 SymbolicLinkName。

## <a name="span-id2_set_registry_valuesspanspan-id2_set_registry_valuesspan2-set-registry-values"></a><span id="2._set_registry_values"></span><span id="2._SET_REGISTRY_VALUES"></span>2. 设置注册表值


音频驱动程序调用 IoOpenDeviceInterfaceRegistryKey 来获取设备接口注册表项的句柄。 音频驱动程序将参数设置为 IoOpenDeviceInterfaceRegistryKey，如下所示。

SymbolicLinkName 是在上一步中从 IoRegisterDeviceInterface 返回的字符串。

\_如果驱动程序) 需要，DesiredAccess 设置为密钥写入 (或其他值。

成功完成上述步骤后，DeviceInterfaceKey 将返回已打开的注册表项句柄。 音频驱动程序：

-   调用 ZwSetValueKey 以设置注册表值

-   通过调用 ZwClose 关闭注册表项句柄

**注意**  如果驱动程序需要在注册表子项中设置值，则驱动程序将调用 ZwCreateKey 来创建该子项。 准备调用 ZwCreateKey 时，驱动程序：
-   调用 InitializeObjectAttributes，并将 ObjectName 设置为子项路径

-   将属性设置为不 \_ 区分大小写的属性 \_ |OBJ \_ 内核 \_ 句柄

-   将 RootDirectory 设置为 IoOpenDeviceInterfaceRegistryKey 返回的句柄

-   调用 ZwClose 以关闭通过调用 ZwCreateKey 创建的任何句柄

 

## <a name="span-id3_set_propertiesspanspan-id3_set_propertiesspan3-set-properties"></a><span id="3._set_properties"></span><span id="3._SET_PROPERTIES"></span>3. 设置属性


音频驱动程序调用 IoSetDeviceInterfacePropertyData 来设置属性。 音频驱动程序将参数设置为 IoSetDeviceInterfacePropertyData，如下所示： 
- SymbolicLinkName 是从 IoRegisterDeviceInterface 返回的字符串。 
- 其余参数取决于所设置的特定属性。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[相关的设计指南](related-design-guidelines.md)  



