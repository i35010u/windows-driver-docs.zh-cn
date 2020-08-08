---
title: 远程显示驱动程序
description: 远程显示驱动程序基于 Windows 2000 镜像驱动程序模型，用于在远程会话中呈现桌面。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ca416a7e5dfadb01b2f7ed9241c6a827555fbee
ms.sourcegitcommit: 799eda3332a500427d7a82ef513fe367dbf72e41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "88001390"
---
# <a name="remote-display-drivers"></a>远程显示驱动程序

> [!NOTE]
>
> Windows 10 版本2004中已删除对 GDI 远程显示驱动程序的支持。 但是，仍然可以通过构建自定义[远程协议提供](/windows/win32/termserv/creating-a-custom-remote-protocol)程序和[间接显示驱动](indirect-display-driver-model-overview.md)程序来创建远程显示解决方案。

*远程显示驱动程序*基于 Windows 2000[镜像驱动程序](mirror-drivers.md)模型，用于在远程会话中呈现桌面。

若要成功地安装和运行 Windows 8，远程显示驱动程序必须仅实现 (DDIs) 的以下设备驱动程序接口，不能再实现。

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
