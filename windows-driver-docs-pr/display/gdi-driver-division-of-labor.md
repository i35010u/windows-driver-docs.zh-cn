---
title: GDI/驱动程序的工作划分
description: GDI/驱动程序的工作划分
ms.assetid: 280addc6-3fc2-4763-ba87-5e9c5e83d22e
keywords:
- GDI WDK Windows 2000 显示、 驱动程序的工作划分
- 显示图形驱动程序 WDK Windows 2000，驱动程序的工作划分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a145a618f69ff4649bdabea2760d5548341401e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533783"
---
# <a name="gdidriver-division-of-labor"></a>GDI/驱动程序的工作划分


## <span id="ddk_gdi_2f_driver_division_of_labor_gg"></span><span id="DDK_GDI_2F_DRIVER_DIVISION_OF_LABOR_GG"></span>


若要了解图形驱动程序设计，务必了解的 GDI 和驱动程序，以及它们如何协商的角色。 GDI，其增强功能，可以处理许多以前需要图形驱动程序的操作。 GDI 还有负责管理数据结构的关键图形操作，如图面，尽管每个图形驱动程序必须具有对其进行访问。

 

 





