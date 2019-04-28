---
title: 图像处理
description: 图像处理
ms.assetid: 84e10fcc-3998-434c-922a-65b42dccbdaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e7a95b973a97bc44c3149209188e4d25216072
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335444"
---
# <a name="image-processing"></a>图像处理





某些微型驱动程序中特定的扫描程序微型驱动程序，需要图像处理层。 此层是从静态图像设备获取的数据需要一些操作，然后再传递到应用程序，才必需的。

如果从设备获取的原始数据需要不做进一步处理，可以省略图像处理层。

如果任何图像操作是必需的 Microsoft 建议使用 GDI + 中 WIA 微型驱动程序。

### <a name="using-gdi-in-a-wia-driver"></a>使用 GDI + 中 WIA 驱动程序

GDI + 是一个库，提供二维图像操作例程。 库提供了用于修改图像特性以及旋转和调整大小的机制。

若要使用 GDI + 中 WIA 微型驱动程序，请确保 GDI + 正确初始化。 GDI + WIA 微型驱动程序将创建并加载时可以进行初始化。 此外，请确保 WIA 驱动程序，包括*Gdiplus.h*以及指向*Gdiplus.lib*库。

关于 GDI + 的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




