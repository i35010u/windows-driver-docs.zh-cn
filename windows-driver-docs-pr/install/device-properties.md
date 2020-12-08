---
title: 设备属性
description: 设备属性
keywords:
- 设备安装 WDK，设备属性
- 设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e91a9963271e5bfab50203b77786269b217d1f57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782837"
---
# <a name="device-properties"></a>设备属性


设备属性编入设备实例、 [设备安装程序类](./overview-of-device-setup-classes.md)、 [设备接口类](./overview-of-device-interface-classes.md)和设备接口的属性。 这些属性描述了组件的功能及其在 Windows 操作系统中的配置。

Windows Vista 和更高版本的 Windows 支持 [统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md) ，该模型定义了如何表示这些设备属性。

Microsoft Windows Server 2003、Windows XP 和 Windows 2000 不支持此统一设备属性模型。 但是，这些早期版本的 Windows 版本支持依赖于组件类型和属性类型的相应 [设备属性表示形式](device-property-representations--windows-server-2003--windows-xp--and-.md) 。 为了保持与早期版本的 windows 版本的兼容性，Windows Vista 和更高版本的 Windows 还支持这些以前的表示形式。 但是，你应该使用 Windows Vista 和更高版本的统一设备属性模型来访问设备属性。

有关统一设备属性模型的组件（包括设备属性功能、系统定义的设备属性、数据结构和 INF 文件指令）的参考信息，请参阅 [设备属性参考](/previous-versions/ff541483(v=vs.85))。

 

