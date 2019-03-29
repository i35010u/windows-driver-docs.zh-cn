---
title: DC 原点
description: DC 原点
ms.assetid: 7e997f6b-fec4-4aa4-b0ed-0d02cb3f844d
keywords:
- DC 源 WDK GDI
- 图面协商 WDK GDI，DC 源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c81d8a2f2c936af10d8bb7c5725525a1b707a204
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567587"
---
# <a name="dc-origin"></a>DC 原点


## <span id="ddk_dc_origin_gg"></span><span id="DDK_DC_ORIGIN_GG"></span>


应用程序所需保留 2²⁷ 数组内的其图形 2²⁷ 像素。 设备空间 DDI 级别，因为窗口管理器可能会抵消在两个签名 27 位坐标，通过应用程序的坐标系统的图形在有额外的大小*DC 源*。 DC 原点看不到驱动程序，并驱动程序标识的图形坐标仅后应用偏移量。

 

 





