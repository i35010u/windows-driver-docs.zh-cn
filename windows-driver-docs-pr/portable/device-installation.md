---
Description: Device Installation
title: 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6c45211f6367ee1eb74c40863f29441dc9a36ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575349"
---
# <a name="device-installation"></a>设备安装


WPD 驱动程序属于 UMDF （Windows 驱动程序框架 (WDF)-用户-模式驱动程序框架） 兼容的驱动程序。 因此，它们将安装使用 Windows 即插即用和播放 (PnP) 基础结构。

此外，还有各种方法来创建即插即用体验在不是传统上即插即用的总线上 — 例如，使用 PNP-X 的适用于网络设备。 这支持通过任意总线的设备的发现，并允许执行之前作为安装的即插即用组件。

在系统上安装设备驱动程序后，客户端将使用 WPD Api 来枚举所有已安装和当前处于活动状态 WPD 设备。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





