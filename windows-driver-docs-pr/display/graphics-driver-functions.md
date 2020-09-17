---
title: 图形驱动程序函数
description: 图形驱动程序函数
ms.assetid: 2e8725a1-2d98-472d-b8ec-8f451272fe77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50170d09cf29feb2e035159d4c681eb39f71916e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716030"
---
# <a name="graphics-driver-functions"></a>图形驱动程序函数


## <span id="ddk_graphics_driver_functions_gg"></span><span id="DDK_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


下面的主题介绍了驱动程序入口点函数、根据需要将它们分类、在某些情况下需要和可选。

[必需的图形驱动程序函数](required-graphics-driver-functions.md)

[在不同的条件下需要的图形驱动程序函数](conditionally-required-graphics-driver-functions.md)

[可选的图形驱动程序函数](optional-graphics-driver-functions.md)

当设备驱动程序返回错误时，它通常应调用 GDI [**EngSetLastError**](/windows/win32/api/winddi/nf-winddi-engsetlasterror) 函数以报告扩展的错误代码。 然后，应用程序可以检索错误代码。

 

