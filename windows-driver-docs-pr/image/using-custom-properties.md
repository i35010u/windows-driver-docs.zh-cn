---
title: 使用自定义属性
description: 使用自定义属性
ms.assetid: cf4e728f-7900-4849-ab1c-135f9fec9713
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc1a7f312ca3afd88c5272e492fd7d200e72789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840729"
---
# <a name="using-custom-properties"></a>使用自定义属性





WIA 驱动程序可以定义自己的自定义属性。 调用方可以像处理普通的 WIA 属性一样操作自定义属性。 但是，只有应用程序或自定义 UI 模块可以访问这些自定义属性。

WIA 驱动程序应将自定义属性定义为具有由 WIA 偏移的属性标识符\_专用\_DEVPROP 用于设备属性，并将 WIA\_PRIVATE\_ITEMPROP 用于常规项属性，如内部[**IWiaMiniDrv：:d rvInitItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)。 有关详细信息，请参阅[定义自定义属性](defining-custom-properties.md)。

可以通过两种方法将自定义参数传递给 WIA 驱动程序。

第一种方法是使用**IWiaItemExtras：： Escape**方法（如 Microsoft Windows SDK 文档中所述）。 这类似于[**IStiUSD：： Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)方法，但它允许调用方直接使用 WIA，而不是使用 STI 方法。 使用**IWiaItemExtras：： Escape**，可以将任何信息传递给驱动程序，驱动程序可以将任何信息传回。 WIA 服务仅管理在调用方和驱动程序之间传递的缓冲区。

第二种方法是使用自定义属性。 使用**IWiaItemExtras：： Escape**方法比使用自定义 wia 属性更灵活，但使用自定义 wia 属性可以在项的属性流中存储信息，以便驱动程序可以在另一次读取信息。

下面两个示例代码片段演示如何使用自定义属性将自定义参数传递给驱动程序和从驱动程序传递自定义参数。

[用于创建自定义属性的示例代码](sample-code-to-create-custom-properties.md)

[用于设置自定义属性的示例代码](sample-code-to-set-custom-properties.md)

 

 




