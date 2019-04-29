---
title: 使用 AF、VC、SAP 和参与方
description: 使用 AF、VC、SAP 和参与方
ms.assetid: 4bf736a9-1236-4322-85f0-5d3ab7b8c549
keywords:
- 面向连接的 NDIS WDK，创建的实体
- 网络、 创建的实体的 CoNDIS WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e1eec5a3be271ce55b994dd2d8d39e8d5643ed8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372169"
---
# <a name="using-afs-vcs-saps-and-parties"></a>使用 AF、VC、SAP 和参与方





面向连接的驱动程序创建和使用实体包括地址系列 (AFs)、 虚拟连接 (VCs)、 服务访问点 (SAPs) 和参与方。

当面向连接的驱动程序注册 AF 或创建 VC、 SAP、 或参与方时，它将指针传递到该实体到 NDIS 其本地上下文区域。 NDIS 然后返回到驱动程序 （以及其他合适的面向连接的驱动程序） 将表示新注册的 AF 或新创建 VC、 SAP、 或参与方的句柄。

以下主题介绍了面向连接的驱动程序创建和使用的实体：

[地址系列](address-families.md)

[虚拟连接](virtual-connections.md)

[服务访问点](service-access-points.md)

[参与方](parties.md)

 

 





