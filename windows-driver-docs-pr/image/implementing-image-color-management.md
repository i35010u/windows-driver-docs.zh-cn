---
title: 实现图像颜色管理
description: 实现图像颜色管理
ms.assetid: b3184a8b-4f32-4cb0-8f68-777d85110142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a3afdc65b1bd70b5f235935b572587cf1289b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362079"
---
# <a name="implementing-image-color-management"></a>实现图像颜色管理





WIA 依赖于在 Microsoft Windows 中提供的图像颜色管理 (ICM) 系统。 ICM 是 Microsoft Windows SDK 文档中所述。

最佳的应用程序兼容性，所有微型驱动程序应在 sRGB 颜色空间中返回数据。 如果设备本机生成不同的颜色空间中的数据，微型驱动程序应使用 ICM 函数以将其输出映射到 sRGB。 某些应用程序实现 ICM，可能想要在本机颜色空间中检索数据。 微型驱动程序可以允许使用此功能通过在安装程序信息 (INF) 文件中指定的本机颜色空间，并指定有效的值为 1 [ **WIA\_IPA\_应用\_颜色\_映射**](https://msdn.microsoft.com/library/windows/hardware/ff551521)属性。

当应用程序的属性设置为 1 时，微型驱动程序应停止到 sRGB 映射，并允许应用程序处理的映射。 应用程序使用的当前值[ **WIA\_IPA\_ICM\_配置文件\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff551571)属性作为设备中的数据的配置文件。 用户使用的系统对话框将属性设置，它不应更改的微型驱动程序。

 

 




