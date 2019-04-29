---
title: 使用自定义属性
description: 使用自定义属性
ms.assetid: cf4e728f-7900-4849-ab1c-135f9fec9713
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec7fc3e78b0981fbb0e903c102e897ed247de05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383703"
---
# <a name="using-custom-properties"></a>使用自定义属性





WIA 驱动程序可以定义自己的自定义属性。 调用方可以操作自定义属性，就像正常 WIA 属性。 但是，只有在应用程序或自定义 UI 模块可以访问这些自定义属性。

WIA 驱动程序应定义要具有偏移的 WIA 的属性标识符的自定义属性\_私有\_DEVPROP 设备属性和使用 WIA\_专用\_ITEMPROP 正常项属性，此类内[ **IWiaMiniDrv::drvInitItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff544989)。 有关详细信息，请参阅[定义的自定义属性](defining-custom-properties.md)。

有两种方法将自定义参数传递给 WIA 驱动程序。

第一个选项是使用**IWiaItemExtras::Escape**方法 （Microsoft Windows SDK 文档中所述）。 它类似于[ **IStiUSD::Escape** ](https://msdn.microsoft.com/library/windows/hardware/ff543815)方法，但它允许调用方 WIA 直接使用，而不是使用 STI 方法。 使用**IWiaItemExtras::Escape**，可以将任何信息传递给该驱动程序，并驱动程序可以将传递回的任何信息。 WIA 服务管理调用方和驱动程序之间传递这些缓冲区。

第二个选项是使用自定义属性。 使用**IWiaItemExtras::Escape**方法比使用 WIA 的自定义属性，更灵活，但自定义 WIA 属性，您可以将信息存储在项的属性流，以使该驱动程序可以读取在其他信息时间。

以下两个示例代码段演示如何使用自定义属性来传递与您的驱动程序的自定义参数。

[若要创建自定义属性的示例代码](sample-code-to-create-custom-properties.md)

[若要设置自定义属性的示例代码](sample-code-to-set-custom-properties.md)

 

 




