---
title: 远程显示驱动程序
description: 远程显示器驱动程序基于 Windows 2000 镜像驱动程序模型，用于在远程会话中呈现到桌面。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9004d7a0d53ff2ac5438e8d41e27b2580a44ab0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386442"
---
# <a name="remote-display-drivers"></a>远程显示驱动程序


一个*远程显示器驱动程序*基于 Windows 2000[镜像驱动程序](mirror-drivers.md)模型和用于呈现到桌面的远程会话中。

若要成功安装并运行从 Windows 8 开始，远程显示器驱动程序必须实现仅以下设备驱动程序接口 (DDIs) 和没有更多。

-   [**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)
-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)
-   [**DrvCompletePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)
-   [**DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)
-   [**DrvDisableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)
-   [**DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)
-   [**DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)
-   [**DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)
-   [**DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)
-   [**DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)
-   [**DrvGetModes**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetmodes)
-   [**DrvMovePointer**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)
-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)
-   [**DrvSetPointerShape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)

 

 





