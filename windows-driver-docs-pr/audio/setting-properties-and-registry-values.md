---
title: 设置属性和注册表值
description: 设置属性和注册表值本主题介绍如何端口类音频驱动程序可以设置属性和即插即用设备接口的注册表值。
ms.assetid: EB6E9673-4A87-45D9-A334-8C2AE33A7581
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143c95f099afeb8b40c6df1e5c5d7eb7ab51fb2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328641"
---
# <a name="setting-properties-and-registry-values"></a>设置属性和注册表值


设置属性和注册表值本主题介绍如何端口类音频驱动程序可以设置属性和即插即用设备接口的注册表值。

端口类音频驱动程序，Portcls 必须执行以下步骤来正确地注册设备接口和设置所需的值。

## <a name="span-id1registerthedeviceinterfacespanspan-id1registerthedeviceinterfacespan1-register-the-device-interface"></a><span id="1._register_the_device_interface"></span><span id="1._REGISTER_THE_DEVICE_INTERFACE"></span>1.注册设备接口


在调用前 PcRegisterSubdevice 子设备，该驱动程序可以直接调用 IoRegisterDeviceInterface 注册 KSCATEGORY\_音频接口。 这使该驱动程序有机会 PcRegisterSubdevice 注册，并启用这些接口之前设置的设备接口的接口属性和注册表值。

音频驱动程序设置的参数 IoRegisterDeviceInterface，如下所示。

-   PhysicalDeviceObject 参数是 PDEVICE\_音频驱动程序可以检索从 PcGetPhysicalDeviceObject 函数的对象。

-   InterfaceClassGuid 设置为接口的类 GUID。

-   ReferenceString 是与音频驱动程序将传递给 PcRegisterSubdevice 名称参数相同。

前面的任务已成功完成后，IoRegisterDeviceInterface 返回已注册的接口 SymbolicLinkName。

## <a name="span-id2setregistryvaluesspanspan-id2setregistryvaluesspan2-set-registry-values"></a><span id="2._set_registry_values"></span><span id="2._SET_REGISTRY_VALUES"></span>2.设置注册表值


音频驱动程序调用 IoOpenDeviceInterfaceRegistryKey 若要获取的句柄设备接口注册表项。 音频驱动程序设置的参数 IoOpenDeviceInterfaceRegistryKey，如下所示。

SymbolicLinkName 是 IoRegisterDeviceInterface 从上一步中返回的字符串。

DesiredAccess 设置为键\_写入 （或其他值，如果所需的驱动程序）。

已成功完成上述步骤后，DeviceInterfaceKey 返回打开的注册表项句柄。 音频驱动程序：

-   调用 ZwSetValueKey 设置注册表值

-   通过调用 ZwClose 关闭注册表项句柄

**请注意**  驱动程序所需注册表子项中设置的值，如果该驱动程序调用 ZwCreateKey 若要创建子项。 当正在准备调用 ZwCreateKey，驱动程序：
-   调用 InitializeObjectAttributes，并将对象名称设置为子项路径

-   将属性设置为 OBJ\_用例\_INSENSITIVE |OBJ\_内核\_处理

-   设置 RootDirectory 为 IoOpenDeviceInterfaceRegistryKey 返回的句柄

-   调用 ZwClose 关闭任一句柄通过调用 ZwCreateKey 创建

 

## <a name="span-id3setpropertiesspanspan-id3setpropertiesspan3-set-properties"></a><span id="3._set_properties"></span><span id="3._SET_PROPERTIES"></span>3.设置属性


音频驱动程序调用 IoSetDeviceInterfacePropertyData 设置属性。 音频驱动程序设置的参数 IoSetDeviceInterfacePropertyData，如下所示： 
- SymbolicLinkName 是从 IoRegisterDeviceInterface 返回的字符串。 
- 剩余的参数取决于要设置的特定属性。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[相关的设计准则](related-design-guidelines.md)  



