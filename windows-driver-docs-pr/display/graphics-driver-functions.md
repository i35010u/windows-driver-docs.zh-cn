---
title: 图形驱动程序函数
description: 图形驱动程序函数
ms.assetid: 2e8725a1-2d98-472d-b8ec-8f451272fe77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e90633c56ad388e2f0735a604a7eaa1a98e6665
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371449"
---
# <a name="graphics-driver-functions"></a>图形驱动程序函数


## <span id="ddk_graphics_driver_functions_gg"></span><span id="DDK_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


按照的主题介绍分类为必需，在某些情况下，必需和可选的驱动程序入口点函数。

[所需的图形驱动程序函数](required-graphics-driver-functions.md)

[有条件地需要图形驱动程序函数](conditionally-required-graphics-driver-functions.md)

[可选的图形驱动程序函数](optional-graphics-driver-functions.md)

当设备驱动程序返回错误时，则通常应调用 GDI [ **EngSetLastError** ](https://msdn.microsoft.com/library/windows/hardware/ff565015)函数来报告扩展的错误代码。 然后，应用程序可以检索错误代码。

 

 





