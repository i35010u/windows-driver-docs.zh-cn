---
title: WIA 简介
description: WIA 简介
ms.assetid: 51674b06-f9d5-4e35-a2ec-9d6cc0a09ef3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74947d485e7667bd185c6fa4a0db3f2c14da1b9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327149"
---
# <a name="introduction-to-wia"></a>WIA 简介





Microsoft Windows 图像采集 (WIA) 接口是应用程序编程接口 (API) 和设备驱动程序接口 (DDI)。 WIA API 设计用于允许应用程序：

-   强大、 稳定的环境中运行。

-   最大程度减少互操作性问题。

-   枚举可用的图像获取设备。

-   同时创建多个设备的连接。

-   标准且可扩展的方式查询设备的属性。

-   获取使用标准和高性能的传输机制的设备数据。

-   在数据传输之间维护映像属性。

-   收到通知的各种设备事件。

WIA DDI 旨在最小化的硬件供应商必须编写，同时保持灵活地创建单个解决方案的代码量。 这是通过实现：

-   提供执行大多数驱动程序操作的标准设备服务库。

-   提升行业设备通信标准，例如图片传输协议 (PTP)，因此该 WIA 驱动程序支持大多数 WIA 的设备。

本部分介绍以下几个方面的 WIA 的简要概述：

[WIA 体系结构概述](wia-architecture-overview.md)

[WIA 核心组件](wia-core-components.md)

 

 




