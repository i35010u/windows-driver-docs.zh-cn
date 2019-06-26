---
title: 提供 COM 接口
description: 提供 COM 接口
ms.assetid: c3e1578e-26f1-4fe3-b56d-a2baacb8e4c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8483cca790314125087e10be0941a71c45dad1ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374314"
---
# <a name="providing-a-com-interface"></a>提供 COM 接口





WIA 微型驱动程序必须支持**IWiaMiniDrv**， **IStiUSD**，并**IUnknown**接口会被识别和 WIA 服务加载。 以下接口标识符应添加到 WIA 驱动**QueryInterface**方法：

-   **IID\_IWiaMiniDrv** -的接口标识符[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)，标准 WIA 接口用来访问特定于 WIA 的功能。

-   **IID\_IStiUSD** -的接口标识符[IStiUSD 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)，标准 STI 接口用来访问 WIA 驱动程序的 STI 功能

-   **IID\_IUnknown** -的接口标识符**IUnknown**接口，Microsoft Windows SDK 文档中定义的标准 COM 接口。

微型驱动程序导出到 WIA 服务调用微型驱动程序的响应中的这些接口标识符**QueryInterface**方法。

有关如何实现这些接口的示例，请参阅*wiascanr*扫描程序示例微型驱动程序文件*wiascanr.h*， *iwiaminidrv.cpp*和*istiusd.cpp 或 s*ee *wiacam*照相机示例微型驱动程序文件*IWiaMiniDrv.cpp*并*IStiUSD.cpp*。

 

 




