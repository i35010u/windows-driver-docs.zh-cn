---
description: 设备安装
title: 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8922cfa79cbf98bd6deb89e87277edd2fd5b7f16
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969556"
---
# <a name="device-installation"></a>设备安装


WPD 驱动程序 (Windows 驱动程序框架 (WDF) 用户模式驱动程序框架) 兼容的驱动程序。 因此，它们将使用 Windows 即插即用 (PnP) 基础结构来安装。

还可以通过多种方式在传统上不使用 PnP 的总线上创建 PnP 体验，例如，将 Pnp-x 用于网络设备。 这样可以通过任意总线发现设备，并允许 PnP 组件像以前一样执行安装。

在系统上安装设备的驱动程序后，客户端将使用 WPD Api 来枚举所有已安装的和当前处于活动状态的 WPD 设备。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





