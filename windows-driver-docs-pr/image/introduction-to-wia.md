---
title: WIA 简介
description: WIA 简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e772a0949dd153a82062df787432eafcc1a86714
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837247"
---
# <a name="introduction-to-wia"></a>WIA 简介





Microsoft Windows 映像采集 (WIA) 接口既是 () API 的应用程序编程接口，又是 (DDI) 的设备驱动程序接口。 WIA API 旨在允许应用程序：

-   在稳定稳定的环境中运行。

-   最大程度减少互操作性问题。

-   枚举可用的映像获取设备。

-   同时创建与多个设备的连接。

-   以标准且可扩展的方式查询设备的属性。

-   使用标准和高性能传输机制获取设备数据。

-   跨数据传输维护图像属性。

-   收到各种设备事件的通知。

WIA DDI 旨在最大程度地减少硬件供应商必须编写的代码量，同时保持创建单个解决方案的灵活性。 这是通过以下方式实现的：

-   提供执行大多数驱动程序操作的标准设备服务库。

-   提升行业设备通信标准（如图片传输协议 (PTP) ），使一个 WIA 驱动程序支持大多数 WIA 设备。

本部分提供以下几个方面的 WIA 概述：

[WIA 体系结构概述](wia-architecture-overview.md)

[WIA 核心组件](wia-core-components.md)

 

 




