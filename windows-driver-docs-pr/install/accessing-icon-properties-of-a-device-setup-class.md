---
title: 访问设备安装程序类的图标属性
description: 访问设备安装程序类的图标属性
ms.assetid: 082b23ee-8f5c-41ad-9bb1-1437b71aa921
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2a8c1acb41e6d523314f84c9dee8d5bf89bb1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385121"
---
# <a name="accessing-icon-properties-of-a-device-setup-class"></a>访问设备安装程序类的图标属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备安装程序类属性](accessing-device-setup-class-properties.md)表示图标的设备安装程序类的属性。 统一的设备属性模型使用[ **DEVPKEY_DeviceClass_Icon**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-icon) [属性键](property-keys.md)并[ **DEVPKEY_DeviceClass_IconPath** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-iconpath)属性键来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持这些设备安装程序类属性。 但是，这些早期版本的 Windows 支持下列机制来检索有关设备安装程序类图标的信息：

-   调用[ **SetupDiLoadClassIcon** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)要检索其索引中的设备安装程序类的最小化图标*MiniIconIndex*输出参数。 然后，可以传递到的检索到的最小化图标的索引[ **SetupDiDrawMiniIcon** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)绘制指定的设备上下文中检索到的类图标的最小化图标。

-   调用 SetupDiLoadClassIcon 加载设备的安装程序类的上下文中的调用方的大图标并将句柄返回给调用方的大图标。

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性，还支持这些机制来访问设备安装程序类的图标。 但是，应使用属性键来访问在 Windows Vista 和更高版本中的图标属性。

 

 





