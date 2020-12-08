---
title: 使用 AF、VC、SAP 和参与方
description: 使用 AF、VC、SAP 和参与方
keywords:
- 面向连接的 NDIS WDK，已创建实体
- CoNDIS WDK 网络，已创建实体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b57b0d8f16699544f4bb18fc0bf29632658ba17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797863"
---
# <a name="using-afs-vcs-saps-and-parties"></a>使用 AF、VC、SAP 和参与方





面向连接的驱动程序创建和使用实体，包括地址系列 (AFs) ，虚拟连接 (VCs) ，服务访问点 (Sap) 和参与方。

当面向连接的驱动程序注册 AF 或创建 VC、SAP 或参与方时，它会将该实体的本地上下文区域的指针传递到 NDIS。 然后，NDIS 返回到驱动程序 (和其他面向连接的其他驱动程序) 表示新注册的 AF 的句柄或新创建的 VC、SAP 或参与方。

以下主题描述了面向连接的驱动程序创建和使用的实体：

[地址系列](address-families.md)

[虚拟连接](virtual-connections.md)

[服务接入点](service-access-points.md)

[参与方](parties.md)

 

 





