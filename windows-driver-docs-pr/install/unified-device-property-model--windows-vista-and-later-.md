---
title: 统一的设备属性模型
description: 统一的设备属性模型
keywords:
- 设备属性 WDK 设备安装，统一设备属性模型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8f3e72137e599dc33f3eadd804bc29c95a3dd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804109"
---
# <a name="unified-device-property-model"></a>统一的设备属性模型


Windows Vista 和更高版本的 Windows 支持统一的设备属性模型，这反映了 *设备实例*、 [设备安装程序类](./overview-of-device-setup-classes.md)、 [设备接口类](./overview-of-device-interface-classes.md)和 *设备接口* 的系统配置。 有关统一设备属性模型的信息，请参阅以下主题：

-   [系统定义的设备属性](system-defined-device-properties2.md)

-   [创建自定义设备属性](creating-custom-device-properties.md)

-   [属性键](property-keys.md)

-   [属性数据类型标识符](property-data-type-identifiers.md)

-   [属性值要求](property-value-requirements.md)

-   [属性和相关的系统定义项](properties-and-related-system-defined-items.md)

-   [可修改设备属性的 INF 文件条目值](inf-file-entry-values-that-modify-device-properties--windows-vista-and.md)

-   [使用 SetupAPI 访问设备属性](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)

-   [使用 INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)

统一设备属性模型中的许多系统定义的设备属性具有相应的表示形式，可用于访问 Microsoft Windows Server 2003、Windows XP 和 Windows 2000 上的相同信息。 为了保持与早期版本的 windows 版本的兼容性，Windows Vista 和更高版本的 Windows 还支持这些表示形式。 但是，你应该使用 Windows Vista 和更高版本的统一设备属性模型来访问设备属性。

 

