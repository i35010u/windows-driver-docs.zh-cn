---
title: 访问共同安装程序的设备安装程序类的新注册表条目值
description: 访问设备安装程序类的辅助安装程序注册表项值
ms.assetid: 731d29df-6fdd-4f25-9758-d7306fef7ec0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f611af9896f2481a11c3cd41086b16bf8a15bf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386045"
---
# <a name="accessing-the-co-installers-registry-entry-value-of-a-device-setup-class"></a>访问设备安装程序类的辅助安装程序注册表项值


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备安装程序类属性](accessing-device-setup-class-properties.md)表示的共同安装程序类安装。 统一的设备属性模型使用[ **DEVPKEY_DeviceClass_ClassCoInstallers**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-classcoinstallers) [属性键](property-keys.md)来表示此属性。

Windows Server 2003、 Windows XP 和 Windows 2000 也支持此属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型的项的属性。 相反，这些版本的 Windows 通过使用相应的系统定义的注册表条目值，表示此属性。 若要保持与这些早期版本的 Windows 兼容性，Windows Vista 和更高版本还支持此系统定义的注册表项值。 但是，应使用的属性键来访问这些属性在 Windows Vista 和更高版本上。

有关如何使用属性键来访问在 Windows Vista 和更高版本上的设备安装程序类属性的信息，请参阅[访问设备类属性 （Windows Vista 和更高版本）](accessing-device-class-properties--windows-vista-and-later-.md)。

在 Windows Server 2003、 Windows XP 和 Windows 2000 上，可以设置或检索此属性通过使用 Windows 注册表函数来访问设备安装程序类的以下注册表项值：

**HLM\\系统\\CurrentControlSet\\控件\\CoDeviceInstallers\\{** <em>设备安装程序类 guid</em> **}** .

有关注册类共同安装程序的信息，请参阅[注册类共同安装程序](registering-a-class-co-installer.md)。

 

 





