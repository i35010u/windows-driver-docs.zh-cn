---
title: 访问友好名称和类名称的设备安装程序类
description: 访问设备安装程序类的友好名称和类名称
ms.assetid: 52775fc6-1c52-4bed-a943-1afcee67e7e9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 168c0b8d9b64ebacba9b21ce5d8f6dd357392a1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386044"
---
# <a name="accessing-the-friendly-name-and-class-name-of-a-device-setup-class"></a>访问设备安装程序类的友好名称和类名称


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备安装程序类属性](accessing-device-setup-class-properties.md)表示的友好名称以及设备安装程序类的类名称。 统一的设备属性模型使用[ **DEVPKEY_DeviceClass_Name**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-name) [属性键](property-keys.md)并[ **DEVPKEY_DeviceClass_ClassName** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-classname)属性键来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 还支持这些设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些版本的 Windows 使用以下机制来检索相应的属性信息：

-   调用[ **SetupDiGetClassDescriptionEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa)检索设备安装程序类的友好名称。

-   调用[ **SetupDiClassNameFromGuid** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)检索设备安装程序类的类名称。

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性，还支持这些机制来访问的友好名称和设备安装程序类的类名称。 但是，应使用属性键来访问这些属性在 Windows Vista 和更高版本。

 

 





