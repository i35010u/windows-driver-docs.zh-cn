---
title: 图形驱动程序函数
description: 图形驱动程序函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7bf79a65b91dda499689e2270936780476d9dd3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825719"
---
# <a name="graphics-driver-functions"></a>图形驱动程序函数


## <span id="ddk_graphics_driver_functions_gg"></span><span id="DDK_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


下面的主题介绍了驱动程序入口点函数、根据需要将它们分类、在某些情况下需要和可选。

[必需的图形驱动程序函数](required-graphics-driver-functions.md)

[在不同的条件下需要的图形驱动程序函数](conditionally-required-graphics-driver-functions.md)

[可选的图形驱动程序函数](optional-graphics-driver-functions.md)

当设备驱动程序返回错误时，它通常应调用 GDI [**EngSetLastError**](/windows/win32/api/winddi/nf-winddi-engsetlasterror) 函数以报告扩展的错误代码。 然后，应用程序可以检索错误代码。

 

