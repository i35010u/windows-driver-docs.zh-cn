---
title: 静态图像设备的颜色管理
description: 静态图像设备的颜色管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f84bb68ea8bed5052f9bfecdd10ee778dead4078
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823181"
---
# <a name="color-management-for-still-image-devices"></a>静态图像设备的颜色管理





供应商应该为每个静止图像设备提供一个或多个颜色配置文件。 颜色配置文件的文件名应包含在供应商提供的 INF 文件中。 如果设备生成 sRGB 数据，则可以指定系统提供的标准颜色配置文件， *SRGB 颜色空间配置文件 icm*。 安装程序将提供的文件名复制到 " [静止图像设备" 的注册表项](registry-entries-for-still-image-devices.md)之一。

如果设备使用其他颜色空间生成图像，则需要使用其他颜色配置文件。 无论你的设备是在其他颜色空间中生成 sRGB 数据还是生成数据，如果你使用的是一种颜色空间，你都可以获得最佳结果。

必须让静止图像设备知道它将其数据发送到的颜色空间。 例如，假设用户在允许修改数据源) 的系统上重置伽玛级别 (。 应用程序将不会意识到此更改。

有关颜色管理的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




