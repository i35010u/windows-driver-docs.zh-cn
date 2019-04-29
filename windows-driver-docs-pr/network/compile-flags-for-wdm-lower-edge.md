---
title: 编译 WDM 下边缘的标志
description: 编译 WDM 下边缘的标志
ms.assetid: 60fbee2a-b8f3-4d1a-95c2-b4962a406065
keywords:
- NDIS WDM 微型端口驱动程序 WDK 网络，编译标志
- NDIS WDM 微型端口驱动程序 WDK 网络、 构建
- NDIS 微型端口驱动程序 WDK 网络，编译标志的下边缘
- WDM 低边缘 WDK 网络，编译标志
- 编译标志 WDK NDIS WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b7fcf5c7f29e17abdb009b6e1b120b9f40bd6a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356916"
---
# <a name="compile-flags-for-wdm-lower-edge"></a>编译 WDM 下边缘的标志





您必须在 NDIS WDM 微型端口驱动程序来生成 NDIS WDM 微型端口驱动程序的源文件中包括以下编译标志：

-   -DNDIS\_WDM=1

    指示 NDIS 相应 WDM 标头文件包含在内。

或者，可以嵌入编译标志开头的微型端口驱动程序的源代码包含 Ndis.h 标头文件之前。

 

 





