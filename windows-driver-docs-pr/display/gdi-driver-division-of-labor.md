---
title: GDI/驱动程序的工作划分
description: GDI/驱动程序的工作划分
keywords:
- GDI WDK Windows 2000 显示屏，驱动程序划分
- 图形驱动程序 WDK Windows 2000 显示、人工的驱动程序划分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3ea407202b058f8aefecb044287dfcfe1d3b389
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817367"
---
# <a name="gdidriver-division-of-labor"></a>GDI/驱动程序的工作划分


## <span id="ddk_gdi_2f_driver_division_of_labor_gg"></span><span id="DDK_GDI_2F_DRIVER_DIVISION_OF_LABOR_GG"></span>


若要理解图形驱动程序设计，必须了解 GDI 和驱动程序的角色及其协商方式。 GDI 具有增强功能，可以处理以前需要图形驱动程序的许多操作。 GDI 还负责管理对图形操作（如表面）至关重要的数据结构，尽管每个图形驱动程序都必须有权访问它们。

 

 





