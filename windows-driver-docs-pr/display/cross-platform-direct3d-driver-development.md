---
title: 跨平台 Direct3D 驱动程序开发
description: 跨平台 Direct3D 驱动程序开发
ms.assetid: 9363e0f9-4a58-4473-969f-eb54d0678632
keywords:
- Direct3D WDK Windows 2000 显示，跨平台开发
- WDK Direct3D 的跨平台开发
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f4b318399ffa6c6d89e69d569b50653c6e6423
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370773"
---
# <a name="cross-platform-direct3d-driver-development"></a>跨平台 Direct3D 驱动程序开发


## <span id="ddk_cross_platform_direct3d_driver_development_gg"></span><span id="DDK_CROSS_PLATFORM_DIRECT3D_DRIVER_DEVELOPMENT_GG"></span>


Microsoft Windows 2000 及更高版本和 Windows 98 / 我 Direct3D DDI 类型不直接兼容，在编译时，由于命名差异和结构和函数成员在每个 DDI 中的某些类型的更改类型。 逻辑上但是，每个 DDI 类型中的等效成员具有相同的用途。

如果你的代码将可移植之间 Windows 2000 及更高版本和 Windows 98 / 我使用*dx95type.h*，Windows Driver Kit (WDK) 和以前的驱动程序开发工具包 (Ddk) 中包含的实用程序文件。 它包含类型定义和映射 Windows 98 之间发生一些命名差异的宏 / Me 和 Windows 2000 以及更高版本的平台，启用常见驱动程序代码才能使用它们之间。

 

 





