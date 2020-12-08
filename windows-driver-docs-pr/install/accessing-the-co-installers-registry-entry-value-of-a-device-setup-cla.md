---
title: 访问设备安装程序类的共同安装程序注册表项值
description: 访问设备安装程序类的辅助安装程序注册表项值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9e149b815e6a7685ee02bf9f4e6eaa3d5e3556
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826213"
---
# <a name="accessing-the-co-installers-registry-entry-value-of-a-device-setup-class"></a>访问设备安装程序类的辅助安装程序注册表项值


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括 [设备安装程序类属性](accessing-device-setup-class-properties.md) ，该属性表示为类安装的共同安装程序。 统一设备属性模型使用 [**DEVPKEY_DeviceClass_ClassCoInstallers**](./devpkey-deviceclass-classcoinstallers.md) [属性键](property-keys.md) 来表示此属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持此属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 通过使用相应的系统定义的注册表项值来表示此属性。 为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本也支持此系统定义的注册表项值。 但是，在 Windows Vista 和更高版本上，你应该使用属性键来访问这些属性。

有关如何使用属性键访问 Windows Vista 和更高版本上的设备安装程序类属性的信息，请参阅 [访问设备类属性 (Windows vista 和更高版本) ](accessing-device-class-properties--windows-vista-and-later-.md)。

在 Windows Server 2003、Windows XP 和 Windows 2000 上，你可以通过使用 Windows 注册表函数访问设备安装程序类的下列注册表项值，来设置或检索此属性：

**HLM \\System \\ CurrentControlSet \\ Control \\ CoDeviceInstallers \\ {**<em>设备安装程序类 guid</em>**}**。

有关注册类共同安装程序的信息，请参阅 [注册类共同安装程序](registering-a-class-co-installer.md)。

 

