---
title: 访问的设备安装程序类的图标属性
description: 访问的设备安装程序类的图标属性
ms.assetid: 082b23ee-8f5c-41ad-9bb1-1437b71aa921
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a13f7e5922ccd2ab98b60a58b2fd6a56077228
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547957"
---
# <a name="accessing-icon-properties-of-a-device-setup-class"></a>访问的设备安装程序类的图标属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备安装程序类属性](accessing-device-setup-class-properties.md)表示图标的设备安装程序类的属性。 统一的设备属性模型使用[ **DEVPKEY_DeviceClass_Icon**](https://msdn.microsoft.com/library/windows/hardware/ff542299) [属性键](property-keys.md)并[ **DEVPKEY_DeviceClass_IconPath** ](https://msdn.microsoft.com/library/windows/hardware/ff542303)属性键来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持这些设备安装程序类属性。 但是，这些早期版本的 Windows 支持下列机制来检索有关设备安装程序类图标的信息：

-   调用[ **SetupDiLoadClassIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff552053)要检索其索引中的设备安装程序类的最小化图标*MiniIconIndex*输出参数。 然后，可以传递到的检索到的最小化图标的索引[ **SetupDiDrawMiniIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff551005)绘制指定的设备上下文中检索到的类图标的最小化图标。

-   调用 SetupDiLoadClassIcon 加载设备的安装程序类的上下文中的调用方的大图标并将句柄返回给调用方的大图标。

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性，还支持这些机制来访问设备安装程序类的图标。 但是，应使用属性键来访问在 Windows Vista 和更高版本中的图标属性。

 

 





