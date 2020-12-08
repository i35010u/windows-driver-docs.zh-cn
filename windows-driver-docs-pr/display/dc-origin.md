---
title: DC 原点
description: DC 原点
keywords:
- DC 来源 WDK GDI
- surface 协商 WDK GDI，DC 原点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbedafe2fa88d96099a0211c47db0b9fc13b05d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819591"
---
# <a name="dc-origin"></a>DC 原点


## <span id="ddk_dc_origin_gg"></span><span id="DDK_DC_ORIGIN_GG"></span>


应用程序需要将其图形保存在2²⁷的数组中，而不是2²⁷像素。 设备空间在图形 DDI 级别具有更大的大小，因为窗口管理器可能会将应用程序的坐标系统偏移一个有符号的27位坐标，即 *DC 原点*。 DC 原点对驱动程序不可见，驱动程序仅在应用偏移量后标识图形坐标。

 

 





