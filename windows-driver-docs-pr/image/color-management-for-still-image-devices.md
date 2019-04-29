---
title: 静态图像设备的颜色管理
description: 静态图像设备的颜色管理
ms.assetid: dfc4afad-221a-436c-9124-981a74f70ee3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0212d7682407b7af814421ca28130485cbee3147
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373224"
---
# <a name="color-management-for-still-image-devices"></a>静态图像设备的颜色管理





供应商应为每个静态图像设备提供一个或多个颜色配置文件。 颜色配置文件的文件名应包含在供应商提供的 INF 文件。 如果你的设备生成 sRGB 数据，则可以指定系统提供的标准颜色配置文件中， *sRGB 颜色空间 Profile.icm*。 安装程序将提供的文件名称复制到其中一个[的注册表项静止图像设备](registry-entries-for-still-image-devices.md)。

如果设备会生成使用另一个颜色空间的映像，您需要使用不同的颜色配置文件。 是否在另一个颜色空间中你的设备生成 sRGB 数据，您将获得最佳结果，如果一致地使用单一颜色空间。

静止图像设备必须意识到它将发送到其数据的颜色空间。 例如，假设用户重置伽马级别 （在上一种允许修改数据源的系统）。 应用程序不会知道这一更改。

有关颜色管理的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




