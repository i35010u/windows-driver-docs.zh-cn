---
title: 远程显示驱动程序
description: 远程显示驱动程序基于 Windows 2000 镜像驱动程序模型，用于在远程会话中呈现桌面。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17698f4291807aa028c0c84cb7e88bbdca9e5809
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715286"
---
# <a name="remote-display-drivers"></a>远程显示驱动程序

> [!NOTE]
>
> Windows 10 版本2004中已删除对 GDI 远程显示驱动程序的支持。 但是，仍然可以通过构建自定义 [远程协议提供](/windows/win32/termserv/creating-a-custom-remote-protocol) 程序和 [间接显示驱动](indirect-display-driver-model-overview.md)程序来创建远程显示解决方案。

*远程显示驱动程序*基于 Windows 2000[镜像驱动程序](mirror-drivers.md)模型，用于在远程会话中呈现桌面。

若要成功地安装和运行 Windows 8，远程显示驱动程序必须仅实现 (DDIs) 的以下设备驱动程序接口，不能再实现。

-   [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode)
-   [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)
-   [**DrvCompletePDEV**](/windows/win32/api/winddi/nf-winddi-drvcompletepdev)
-   [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits)
-   [**DrvDisableDriver**](/windows/win32/api/winddi/nf-winddi-drvdisabledriver)
-   [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev)
-   [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)
-   [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)
-   [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface)
-   [**DrvEscape**](/windows/win32/api/winddi/nf-winddi-drvescape)
-   [**DrvGetModes**](/windows/win32/api/winddi/nf-winddi-drvgetmodes)
-   [**DrvMovePointer**](/windows/win32/api/winddi/nf-winddi-drvmovepointer)
-   [**DrvResetPDEV**](/windows/win32/api/winddi/nf-winddi-drvresetpdev)
-   [**DrvSetPointerShape**](/windows/win32/api/winddi/nf-winddi-drvsetpointershape)