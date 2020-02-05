---
title: 全局导航卫星系统（GNSS）驱动程序概述
description: 使用本指南了解如何通过全局导航卫星系统（GNSS）驱动程序实现 DeviceIoControl Api，以便 HLOS 如 GNSS 适配器可以访问 GNSS 功能。
ms.assetid: 1887097A-C495-4295-9904-B2964F46A81D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bd3e46849d1e4b760d56562e7b2fc262fc1d7b9
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980686"
---
# <a name="global-navigation-satellite-system-gnss-driver-overview"></a>全局导航卫星系统（GNSS）驱动程序概述

使用全球导航卫星系统（GNSS）驱动程序设计指南，可以了解如何使用 GNSS 驱动程序实现**DeviceIoControl** api，以便类似于 GNSS 适配器的高级操作系统组件（HLOS）可以访问所需的 GNSS 功能。

可通过 IHV 增强 GNSS 功能，以更低的功率成本提供位置，或在需要时提供更好的性能。

新的 GNSS 驱动程序由 Ihv 完全拥有和提供，不会在内核模式下运行任何 Microsoft 自有代码。

> [!NOTE]
> Ihv 不能将筛选器驱动程序添加到 GNSS/Location 堆栈。 筛选器驱动程序很难进行调试和维护，因此，一般不建议使用它们。 除此之外，在未来，Microsoft 可能还需要在 GNSS 设备堆栈中添加筛选器驱动程序，以便扩展功能，并将其他筛选器驱动程序用于 Ihv，使体系结构更复杂。

驱动程序遵循适用于函数驱动程序的通用 UMDF 2.0 模型（用户模式驱动程序框架）。 可以使用 KMDF （内核模式驱动程序框架）驱动程序，但强烈建议不要这样做，因为它们增加了平台不稳定的风险，因而更难进行调试，而且不能直接使用用户模式操作系统组件。
本设计指南假定你基本熟悉 UMDF 2.0、Windows 内核模式编程、内核 i/o 管理、电源管理和 PnP 设备堆栈。

## <a name="related-topics"></a>相关主题

[全局导航卫星系统（GNSS）驱动程序要求](gnss-driver-requirements.md)  

[全局导航卫星系统（GNSS）驱动程序体系结构](gnss-driver-architecture.md)  
