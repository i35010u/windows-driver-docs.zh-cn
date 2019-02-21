---
title: 远程显示器驱动程序
description: 远程显示器驱动程序基于 Windows 2000 镜像驱动程序模型，用于在远程会话中呈现到桌面。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd8ff555fc190468902e2b35c285e64eaf91578
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555947"
---
# <a name="remote-display-drivers"></a>远程显示器驱动程序


一个*远程显示器驱动程序*基于 Windows 2000[镜像驱动程序](mirror-drivers.md)模型和用于呈现到桌面的远程会话中。

若要成功安装并运行从 Windows 8 开始，远程显示器驱动程序必须实现仅以下设备驱动程序接口 (DDIs) 和没有更多。

-   [**DrvAssertMode**](https://msdn.microsoft.com/library/windows/hardware/ff556178)
-   [**DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)
-   [**DrvCompletePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556181)
-   [**DrvCopyBits**](https://msdn.microsoft.com/library/windows/hardware/ff556182)
-   [**DrvDisableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556196)
-   [**DrvDisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556198)
-   [**DrvDisableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556200)
-   [**DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)
-   [**DrvEnableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556214)
-   [**DrvEscape**](https://msdn.microsoft.com/library/windows/hardware/ff556217)
-   [**DrvGetModes**](https://msdn.microsoft.com/library/windows/hardware/ff556233)
-   [**DrvMovePointer**](https://msdn.microsoft.com/library/windows/hardware/ff556248)
-   [**DrvResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556276)
-   [**DrvSetPointerShape**](https://msdn.microsoft.com/library/windows/hardware/ff556289)

 

 





