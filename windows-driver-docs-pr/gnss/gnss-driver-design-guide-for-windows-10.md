---
title: 适用于 Windows 10 的全球导航卫星系统 (GNSS) 驱动程序设计指南
description: 介绍适用于全局导航卫星)  (系统的通用 Windows UMDF 2.0 驱动程序的设计要求和体系结构。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef29d5b05dea3a7b772b293d45cc7e42a977390c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783961"
---
# <a name="global-navigation-satellite-system-gnss-driver-design-guide-for-windows-10"></a>适用于 Windows 10 的全球导航卫星系统 (GNSS) 驱动程序设计指南

本指南介绍了适用于 GNSS 的通用 Windows 驱动程序的设计和体系结构， (UMDF 2.0) 适用于 Windows 10 中的汇聚 Windows 位置堆栈。

## <a name="in-this-section"></a>在本节中

| 主题 | 描述 |
| --- | --- |
| [GNSS 驱动程序概述](gnss-driver-overview.md) | 使用 GNSS 驱动程序设计指南来了解如何使用 GNSS 驱动程序实现 **DeviceIoControl** api，使高级操作系统组件 (HLOS) 例如 GNSS 适配器可以访问所需的 GNSS 功能。 |
| [GNSS 驱动程序要求](gnss-driver-requirements.md) | 描述在开发适用于 Windows 10 的 GNSS 驱动程序时要考虑的要求、假设和约束。 |
| [GNSS 驱动程序体系结构](gnss-driver-architecture.md) | 概述了 GNSS UMDF 2.0 驱动程序体系结构和 i/o 注意事项，并讨论了几种类型的跟踪和修复会话。 |
| [GNSS 驱动程序设计](gnss-driver-design.md) | 讨论开发适用于 Windows 10 的 GNSS 驱动程序时要考虑的设计原则，其中包括数据结构、错误报告和驱动程序版本控制。 |
