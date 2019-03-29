---
title: 安装 NDIS-WDM 微型端口驱动程序
description: 安装 NDIS-WDM 微型端口驱动程序
ms.assetid: 7b87d8e3-cefa-49d7-ae66-0c3d771e24ef
keywords:
- NDIS WDM 微型端口驱动程序 WDK 连接网络、 安装
- NDIS 微型端口驱动程序 WDK 网络驱动程序安装的下边缘
- WDM 低边缘 WDK 网络，驱动程序安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a757161240a7ab057329c16392cad5fb71e3f3b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564035"
---
# <a name="installing-ndis-wdm-miniport-drivers"></a>安装 NDIS-WDM 微型端口驱动程序





当实现 NDIS WDM 微型端口驱动程序的安装机制时，您应记住以下各项：

-   创建有关的信息 (INF) 文件**Net**类的网络组件中所述[创建网络 INF 文件](creating-network-inf-files.md)。

-   包含插 (PnP) 标识符 (ID) 的设备，因为通常是任意**Net**类的网络组件; 但是，使这些 Id 特定于设备附加到的总线类型。

 

 





