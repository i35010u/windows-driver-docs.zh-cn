---
title: 访问设备安装程序类的图标属性
description: 访问设备安装程序类的图标属性
ms.assetid: 082b23ee-8f5c-41ad-9bb1-1437b71aa921
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227cc7dc1f510971f2e9cdc7bc06e168e8a8f8e1
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096595"
---
# <a name="accessing-icon-properties-of-a-device-setup-class"></a>访问设备安装程序类的图标属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括 [设备安装程序类属性](accessing-device-setup-class-properties.md) ，这些属性表示设备安装程序类的图标属性。 统一设备属性模型使用 [**DEVPKEY_DeviceClass_Icon**](./devpkey-deviceclass-icon.md) [属性键](property-keys.md) 和 [**DEVPKEY_DeviceClass_IconPath**](./devpkey-deviceclass-iconpath.md) 属性键来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持这些设备安装程序类属性。 但是，这些早期版本的 Windows 确实支持以下机制来检索有关设备安装程序类图标的信息：

-   调用 [**SetupDiLoadClassIcon**](/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon) 可检索 *MiniIconIndex* 输出参数中设备安装程序类的小图标索引。 然后，可以将检索到的小图标索引传递到 [**SetupDiDrawMiniIcon**](/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon) ，以便在指定的设备上下文中绘制检索到的类图标的小图标。

-   调用 SetupDiLoadClassIcon 可在调用方的上下文中加载设备安装程序类的大图标，并向调用方返回大图标的句柄。

为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持这些机制来访问设备安装程序类的图标。 但是，你应该使用属性键访问 Windows Vista 和更高版本中的图标属性。

 

