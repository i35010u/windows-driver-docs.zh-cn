---
title: 安装 NDIS-WDM 微型端口驱动程序
description: 安装 NDIS-WDM 微型端口驱动程序
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，安装
- NDIS 微型端口驱动程序的下边缘 WDK 网络，驱动程序安装
- WDM 低边缘 WDK 网络，驱动程序安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5da661c1bf09eaf8e7f1553084f015265bd7892
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832223"
---
# <a name="installing-ndis-wdm-miniport-drivers"></a>安装 NDIS-WDM 微型端口驱动程序





实现 NDIS-WDM 微型端口驱动程序的安装机制时，应注意以下事项：

-   如 [创建网络 INF 文件](creating-network-inf-files.md)中所述，为网络组件的 **NET** 类 (INF) 文件创建一个信息。

-   包括即插即用 (PnP) 标识符 (ID) 设备通常对网络组件 **的任何网络类的网络** 但是，请将这些 Id 特定于设备附加到的总线类型。

 

 





