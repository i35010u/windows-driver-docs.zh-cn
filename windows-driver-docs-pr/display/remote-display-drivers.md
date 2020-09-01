---
title: 远程显示驱动程序
description: 远程显示驱动程序基于 Windows 2000 镜像驱动程序模型，用于在远程会话中呈现桌面。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d337786877628bdeab873ce64fa9b72ffec38058
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066408"
---
# <a name="remote-display-drivers"></a>远程显示驱动程序

> [!NOTE]
>
> Windows 10 版本2004中已删除对 GDI 远程显示驱动程序的支持。 但是，仍然可以通过构建自定义 [远程协议提供](/windows/win32/termserv/creating-a-custom-remote-protocol) 程序和 [间接显示驱动](indirect-display-driver-model-overview.md)程序来创建远程显示解决方案。

*远程显示驱动程序*基于 Windows 2000[镜像驱动程序](mirror-drivers.md)模型，用于在远程会话中呈现桌面。

若要成功地安装和运行 Windows 8，远程显示驱动程序必须仅实现 (DDIs) 的以下设备驱动程序接口，不能再实现。

-   [**DrvAssertMode**](/windows/desktop/api/winddi/nf-winddi-drvassertmode)
-   [**DrvBitBlt**](/windows/desktop/api/winddi/nf-winddi-drvbitblt)
-   [**DrvCompletePDEV**](/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)
-   [**DrvCopyBits**](/windows/desktop/api/winddi/nf-winddi-drvcopybits)
-   [**DrvDisableDriver**](/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)
-   [**DrvDisablePDEV**](/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)
-   [**DrvDisableSurface**](/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)
-   [**DrvEnablePDEV**](/windows/desktop/api/winddi/nf-winddi-drvenablepdev)
-   [**DrvEnableSurface**](/windows/desktop/api/winddi/nf-winddi-drvenablesurface)
-   [**DrvEscape**](/windows/desktop/api/winddi/nf-winddi-drvescape)
-   [**DrvGetModes**](/windows/desktop/api/winddi/nf-winddi-drvgetmodes)
-   [**DrvMovePointer**](/windows/desktop/api/winddi/nf-winddi-drvmovepointer)
-   [**DrvResetPDEV**](/windows/desktop/api/winddi/nf-winddi-drvresetpdev)
-   [**DrvSetPointerShape**](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)