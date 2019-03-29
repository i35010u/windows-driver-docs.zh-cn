---
title: 设备属性
description: 设备属性
ms.assetid: 87a43865-74bc-412c-9ae2-3ba38589c8f8
keywords:
- 设备安装 WDK、 设备属性
- 设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f02f9b585f56992659a6153bbea8b8e02640e9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567157"
---
# <a name="device-properties"></a>设备属性


设备属性对设备实例的属性[设备安装程序类](device-setup-classes.md)，[设备接口类](device-interface-classes.md)，和设备接口。 这些属性描述该组件及其配置在 Windows 操作系统中的函数。

Windows Vista 和更高版本的 Windows 支持[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)，它定义如何表示这些设备属性。

Microsoft Windows Server 2003、 Windows XP 和 Windows 2000 不支持此模型中统一的设备属性。 但是这些早期的 Windows 版本支持对应[设备属性表示形式](device-property-representations--windows-server-2003--windows-xp--and-.md)依赖的组件类型和属性类型。 为了保持与这些早期的 Windows 版本的兼容性，Windows Vista 和更高版本的 Windows 还支持这些早期的表示形式。 但是，应使用统一的设备属性的模型的 Windows Vista 和更高版本才能访问设备的属性。

有关组件的统一的设备属性模型的参考信息，包括设备属性函数、 系统定义的设备属性、 数据结构和 INF 文件指令，请参阅[设备属性参考](https://msdn.microsoft.com/library/windows/hardware/ff541483).

 

 





