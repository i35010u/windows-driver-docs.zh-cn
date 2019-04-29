---
title: DIRECT3D_VERSION
description: DIRECT3D_VERSION
ms.assetid: 09032f06-d31f-4d9f-80bd-e6b9b8d5cbaa
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，标头文件
- 标头文件 WDK DirectX 8.0
- DIRECT3D_VERSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f1944cb05f34c0b2618caf17d5b630b2bf59d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357963"
---
# <a name="direct3dversion"></a>DIRECT3D\_版本


## <span id="ddk_direct3d_version_gg"></span><span id="DDK_DIRECT3D_VERSION_GG"></span>


DirectX 显示器驱动程序必须支持 DirectX 7.0 和早期版本的 DirectX 运行时。 为此，请务必包括旧的和新的 DirectX 标头，例如*d3d.h*并*d3d8.h*。 但是，这可能会导致问题的预处理器符号 DIRECT3D 定义\_版本。 此预处理器符号头文件中用于指示应包括的结构和函数。 如果 DIRECT3D\_尚未定义版本中，DirectX 标头文件设置的 DIRECT3D 值\_以为设计的最新版本的版本。 因此， *d3d.h*设置 DIRECT3D\_0x0700 的版本和*d3d8.h*设置 DIRECT3D\_0x0800 的版本。 如果*d3d.h*之前在源中包含*d3d8.h*、 未定义 Direct3D 8.0 的新增功能和将导致编译器错误。

若要避免此问题，定义 DIRECT3D\_0x0800 包含任何标头文件之前的版本。 若要在头文件中获取所有必需的符号，包括之前 d3d8.h *winddi.h*或*d3dnthal.h*。

 

 





