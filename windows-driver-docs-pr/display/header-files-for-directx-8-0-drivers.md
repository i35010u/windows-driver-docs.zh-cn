---
title: DirectX 8.0 驱动程序的标头文件
description: DirectX 8.0 驱动程序的标头文件
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，头文件
- 标头文件 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b011c7e95d686734502b0712d036230415e665f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841001"
---
# <a name="header-files-for-directx-80-drivers"></a>DirectX 8.0 驱动程序的标头文件


## <span id="ddk_header_files_for_directx_8_0_drivers_gg"></span><span id="DDK_HEADER_FILES_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


DirectX 8.0 显示器驱动程序的源代码必须包含 *d3d8* 头文件。 标头文件 *d3d8caps* 和 *d3d8types* 包含在 *d3d8* 中。

DirectX 8.0 驱动程序开发工具包 (DDK) 引入了一个名为 *d3dhalex* 的新的仅限 DDI 的头文件。 此标头文件包含可选的帮助程序定义和宏。 目前，此标头包含一些宏，可帮助报表 D3DCAPS8 到运行时。

 

 





