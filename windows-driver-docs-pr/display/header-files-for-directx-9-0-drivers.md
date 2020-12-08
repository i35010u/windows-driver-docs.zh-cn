---
title: DirectX 9.0 驱动程序的标头文件
description: DirectX 9.0 驱动程序的标头文件
keywords:
- 标头文件 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff38599966d19ef48cf997099cf1853dcb8fc661
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838285"
---
# <a name="header-files-for-directx-90-drivers"></a>DirectX 9.0 驱动程序的标头文件


## <span id="ddk_header_files_for_directx_9_0_drivers_gg"></span><span id="DDK_HEADER_FILES_FOR_DIRECTX_9_0_DRIVERS_GG"></span>


DirectX 9.0 显示器驱动程序的源代码必须包含 *d3d9* 头文件。 标头文件 *d3d9caps* 和 *d3d9types* 包含在 *d3d9* 中。

若要支持 DirectX 8.1 和更早版本的 DirectX 运行时，驱动程序的源代码必须包含新旧的 DirectX 标头，例如 *d3d .h*、 *d3d8* 和 *d3d9*。

若要避免生成 DirectX 9.0 版本驱动程序时出现问题，请 \_ 在包含任何标头文件之前在驱动程序的源代码中将 DIRECT3D 版本定义为0x0900。 这样做可以防止 DirectX 9.0 功能丢失，如 [DIRECT3D \_ 版本](direct3d-version.md) 主题中所述。 若要确保生成过程检索头文件中所有必需的符号，请在 *winddi* 或 *d3dnthal* 前面包含 *d3d9* 和 *d3d8* 。

 

 





