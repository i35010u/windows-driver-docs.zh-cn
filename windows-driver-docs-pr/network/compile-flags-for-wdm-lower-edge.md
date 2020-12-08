---
title: 编译 WDM 下边缘的标志
description: 编译 WDM 下边缘的标志
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，编译标志
- NDIS-WDM 微型端口驱动程序 WDK 网络，生成
- NDIS 微型端口驱动程序的下边缘 WDK 网络，编译标志
- WDM 低边缘 WDK 网络，编译标志
- 编译标志 WDK NDIS-WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d76f9838f3c222d24fea8b2a5bfc51049ef521
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817611"
---
# <a name="compile-flags-for-wdm-lower-edge"></a>编译 WDM 下边缘的标志





你必须在 NDIS-WDM 微型端口驱动程序的源文件中包括以下编译标志，以生成 NDIS-WDM 微型端口驱动程序：

-   -DNDIS \_ WDM = 1

    指示 NDIS 包含适当的 WDM 标头文件。

另外，还可以在包含 Ndis .h 头文件之前，将编译标志嵌入到微型端口驱动程序的源代码开头。

 

 





