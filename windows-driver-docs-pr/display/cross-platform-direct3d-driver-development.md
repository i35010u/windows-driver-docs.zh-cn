---
title: 跨平台 Direct3D 驱动程序开发
description: 跨平台 Direct3D 驱动程序开发
keywords:
- Direct3D WDK Windows 2000 显示，跨平台开发
- 跨平台开发 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 964abc6141bc0f7dc87a051b0b7e28681d6d062c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832793"
---
# <a name="cross-platform-direct3d-driver-development"></a>跨平台 Direct3D 驱动程序开发


## <span id="ddk_cross_platform_direct3d_driver_development_gg"></span><span id="DDK_CROSS_PLATFORM_DIRECT3D_DRIVER_DEVELOPMENT_GG"></span>


在编译时，Microsoft Windows 2000 和更高版本和 Windows 98/Me Direct3D DDI 类型不直接兼容，因为它们的命名差异和每个 DDI 类型中结构和函数成员的某些类型更改。 但在逻辑上，每个 DDI 类型中的等效成员都具有相同的用途。

如果你的代码可在 Windows 2000 和更高版本以及 Windows 98/Me 之间移植，请使用 dx95type，这是 Windows 驱动程序工具包 (WDK) 和以前的驱动程序开发工具包 (Ddk) 中包含的实用工具文件 *。* 它包含类型定义和宏，这些类型定义和宏用于映射 Windows 98/Me 与 Windows 2000 及更高版本的平台之间发生的一些命名差异，并允许在它们之间使用常见的驱动程序代码。

 

 





