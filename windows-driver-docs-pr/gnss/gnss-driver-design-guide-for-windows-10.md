---
title: 适用于 Windows 10 的全球导航卫星系统（GNSS）驱动程序设计指南
description: 介绍 Windows 10 中汇聚 Windows 位置堆栈的通用 Windows UMDF 2.0 驱动程序的设计要求和体系结构。
ms.assetid: FD8503DC-A43F-43B2-A1E9-D80778E326F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5690e43ddeaa5982e987e7bad2b1d00874f003cb
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980684"
---
# <a name="global-navigation-satellite-system-gnss-driver-design-guide-for-windows-10"></a>适用于 Windows 10 的全球导航卫星系统（GNSS）驱动程序设计指南

本指南介绍了 Windows 10 中汇聚 Windows 位置堆栈的通用 Windows driver for GNSS （UMDF 2.0）的设计和体系结构。

## <a name="in-this-section"></a>本部分内容

| 主题 | 描述 |
| --- | --- |
| [GNSS 驱动程序概述](gnss-driver-overview.md) | 使用 GNSS 驱动程序设计指南来了解如何使用 GNSS 驱动程序实现**DeviceIoControl** api，以便类似于 GNSS 适配器的高级操作系统组件（HLOS）可以访问所需的 GNSS 功能。 |
| [GNSS 驱动程序要求](gnss-driver-requirements.md) | 描述在开发适用于 Windows 10 的 GNSS 驱动程序时要考虑的要求、假设和约束。 |
| [GNSS 驱动程序体系结构](gnss-driver-architecture.md) | 概述了 GNSS UMDF 2.0 驱动程序体系结构和 i/o 注意事项，并讨论了几种类型的跟踪和修复会话。 |
| [GNSS 驱动程序设计](gnss-driver-design.md) | 讨论开发适用于 Windows 10 的 GNSS 驱动程序时要考虑的设计原则，其中包括数据结构、错误报告和驱动程序版本控制。 |
