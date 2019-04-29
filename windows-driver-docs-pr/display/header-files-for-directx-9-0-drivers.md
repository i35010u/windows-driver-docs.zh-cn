---
title: DirectX 9.0 驱动程序的标头文件
description: DirectX 9.0 驱动程序的标头文件
ms.assetid: b8628c92-0983-4f3a-af64-ef54201ee689
keywords:
- 标头文件 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14cedd7365d61a9808853e33458d38baee90a57f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377958"
---
# <a name="header-files-for-directx-90-drivers"></a>DirectX 9.0 驱动程序的标头文件


## <span id="ddk_header_files_for_directx_9_0_drivers_gg"></span><span id="DDK_HEADER_FILES_FOR_DIRECTX_9_0_DRIVERS_GG"></span>


必须包括 DirectX 9.0 显示器驱动程序的源代码*d3d9.h*标头文件。 标头文件*d3d9caps.h*并*d3d9types.h*中包含*d3d9.h*。

若要支持 DirectX 8.1 和早期版本的 DirectX 运行时，驱动程序的源代码必须包含旧的和新的 DirectX 标头，例如*d3d.h*， *d3d8.h*，和*d3d9.h*.

若要构建 DirectX 9.0 版本驱动程序时，避免出现问题，定义 DIRECT3D\_0x0900 包含任何标头文件之前，驱动程序的源代码中的版本。 这样做会阻止 DirectX 9.0 功能中所述丢失的可能性[DIRECT3D\_版本](direct3d-version.md)主题。 若要确保在生成过程检索标头文件中的所有必需的符号，包括*d3d9.h*并*d3d8.h*之前*winddi.h*或*d3dnthal.h*.

 

 





