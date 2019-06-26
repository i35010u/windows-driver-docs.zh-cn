---
title: 图形驱动程序函数
description: 图形驱动程序函数
ms.assetid: 2e8725a1-2d98-472d-b8ec-8f451272fe77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5cbce883565fa91a1dab5d41ca8e4f1240b15a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379935"
---
# <a name="graphics-driver-functions"></a>图形驱动程序函数


## <span id="ddk_graphics_driver_functions_gg"></span><span id="DDK_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


按照的主题介绍分类为必需，在某些情况下，必需和可选的驱动程序入口点函数。

[所需的图形驱动程序函数](required-graphics-driver-functions.md)

[有条件地需要图形驱动程序函数](conditionally-required-graphics-driver-functions.md)

[可选的图形驱动程序函数](optional-graphics-driver-functions.md)

当设备驱动程序返回错误时，则通常应调用 GDI [ **EngSetLastError** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetlasterror)函数来报告扩展的错误代码。 然后，应用程序可以检索错误代码。

 

 





