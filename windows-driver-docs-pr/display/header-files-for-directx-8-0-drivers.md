---
title: DirectX 8.0 驱动程序的标头文件
description: DirectX 8.0 驱动程序的标头文件
ms.assetid: 716fc6dc-b1e9-4c81-ae84-03f8a91cc47f
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，标头文件
- 标头文件 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d7278e1ba02999b0d433f7d8481a997fb3a1b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378028"
---
# <a name="header-files-for-directx-80-drivers"></a>DirectX 8.0 驱动程序的标头文件


## <span id="ddk_header_files_for_directx_8_0_drivers_gg"></span><span id="DDK_HEADER_FILES_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


必须包括 DirectX 8.0 显示器驱动程序的源代码*d3d8.h*标头文件。 标头文件*d3d8caps.h*并*d3d8types.h*中包含*d3d8.h*。

DirectX 8.0 驱动程序开发工具包 (DDK) 引入了名为新的仅限 DDI 的头文件*d3dhalex.h*。 此标头文件包含可选的帮助器定义和宏。 目前，此标头包含一些宏，以帮助向运行时报告 D3DCAPS8。

 

 





