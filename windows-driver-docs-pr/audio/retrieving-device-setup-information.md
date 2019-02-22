---
title: 检索设备安装程序信息
description: 检索设备安装程序信息
ms.assetid: 95e88e4a-5a31-4d82-99ea-c9a4d7766c0f
keywords:
- 音频适配器 WDK，检索安装信息
- 适配器驱动程序 WDK 音频，检索安装信息
- 端口类音频适配器 WDK，检索安装信息
- 检索设备安装程序信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230312578cde427e1503f6a4b647ce43eece226f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526938"
---
# <a name="retrieving-device-setup-information"></a>检索设备安装程序信息


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


若要从注册表检索安装信息，请适配器驱动程序可以调用[ **PcGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff537701)函数，并且微型端口驱动程序可以调用端口驱动程序[ **IPort::GetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff536941)方法。

对于任一这些调用，调用方选择的安装信息来请求通过设备属性参数设置为以下设备之一类型\_注册表\_属性枚举值从标头文件 wdm.h 中：

-   **DevicePropertyAddress**

-   **DevicePropertyBootConfiguration**

-   **DevicePropertyBootConfigurationTranslated**

-   **DevicePropertyBusNumber**

-   **DevicePropertyBusTypeGuid**

-   **DevicePropertyClassGuid**

-   **DevicePropertyClassName**

-   **DevicePropertyCompatibleIDs**

-   **DevicePropertyDetachability**

-   **DevicePropertyDeviceDescription**

-   **DevicePropertyDriverKeyName**

-   **DevicePropertyEnumeratorName**

-   **DevicePropertyFriendlyName**

-   **DevicePropertyHardwareID**

-   **DevicePropertyInstallState**

-   **DevicePropertyLegacyBusType**

-   **DevicePropertyLocationInformation**

-   **DevicePropertyManufacturer**

-   **DevicePropertyPhysicalDeviceObjectName**

-   **DevicePropertyUINumber**

有关说明 DeviceProperty*Xxx*值更高版本，请参阅[ **IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)。

 

 




