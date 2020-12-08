---
title: 访问设备安装程序类的友好名称和类名
description: 访问设备安装程序类的友好名称和类名称
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f7a4b12cc538ea69acd3b095058da116241a60c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830021"
---
# <a name="accessing-the-friendly-name-and-class-name-of-a-device-setup-class"></a>访问设备安装程序类的友好名称和类名称


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括 [设备安装程序类属性](accessing-device-setup-class-properties.md) ，这些属性表示设备安装程序类的友好名称和类名。 统一设备属性模型使用 [**DEVPKEY_DeviceClass_Name**](./devpkey-deviceclass-name.md) [属性键](property-keys.md) 和 [**DEVPKEY_DeviceClass_ClassName**](./devpkey-deviceclass-classname.md) 属性键来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持以下设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 使用以下机制来检索相应的属性信息：

-   调用 [**SetupDiGetClassDescriptionEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa) 可检索设备安装程序类的友好名称。

-   调用 [**SetupDiClassNameFromGuid**](/windows/win32/api/setupapi/nf-setupapi-setupdiclassnamefromguida) 可检索设备安装程序类的类名。

为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持这些机制来访问设备安装程序类的友好名称和类名。 但是，在 Windows Vista 和更高版本中，你应该使用属性键来访问这些属性。

 

