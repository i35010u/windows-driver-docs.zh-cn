---
title: 图形驱动程序函数
description: 图形驱动程序函数
ms.assetid: 2e8725a1-2d98-472d-b8ec-8f451272fe77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71b5395e0ec3948e0571adb4b1b75b1fcb7bc559
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064190"
---
# <a name="graphics-driver-functions"></a>图形驱动程序函数


## <span id="ddk_graphics_driver_functions_gg"></span><span id="DDK_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


下面的主题介绍了驱动程序入口点函数、根据需要将它们分类、在某些情况下需要和可选。

[必需的图形驱动程序函数](required-graphics-driver-functions.md)

[在不同的条件下需要的图形驱动程序函数](conditionally-required-graphics-driver-functions.md)

[可选的图形驱动程序函数](optional-graphics-driver-functions.md)

当设备驱动程序返回错误时，它通常应调用 GDI [**EngSetLastError**](/windows/desktop/api/winddi/nf-winddi-engsetlasterror) 函数以报告扩展的错误代码。 然后，应用程序可以检索错误代码。

 

