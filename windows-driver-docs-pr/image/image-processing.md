---
title: 图像处理
description: 图像处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80761caf2d529d97e5ce230a73447c42dc146865
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808209"
---
# <a name="image-processing"></a>图像处理





某些微型驱动程序（特定于 scanner 微型驱动程序）需要图像处理层。 仅当从静止图像设备获取的数据需要在将其传递到应用程序之前进行某种操作时，此层才是必需的。

如果从设备获取的原始数据需要进一步处理，则可以省略图像处理层。

如果需要任何图像操作，Microsoft 建议在 WIA 微型驱动程序中使用 GDI +。

### <a name="using-gdi-in-a-wia-driver"></a>在 WIA 驱动程序中使用 GDI +

GDI + 是提供二维图像操作例程的库。 库提供了修改图像属性以及旋转和调整大小的机制。

若要在 WIA 微型驱动程序中使用 GDI +，请确保已正确初始化 GDI +。 当创建并加载 WIA 微型驱动程序时，可以初始化 GDI +。 此外，请确保 WIA 驱动程序包含 *Gdiplus* 和 *Gdiplus* 库的链接。

有关 GDI + 的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




