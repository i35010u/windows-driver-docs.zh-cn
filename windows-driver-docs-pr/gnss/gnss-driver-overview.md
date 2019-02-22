---
title: GNSS 驱动程序概述
description: 使用本指南，了解如何实现 DeviceIoControl Api 使用 GNSS 驱动程序，以便像 GNSS 适配器 HLOS 可以访问 GNSS 功能。
ms.assetid: 1887097A-C495-4295-9904-B2964F46A81D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f5ef80389d7bbb88c9e5c2496439e6a015727a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545576"
---
# <a name="gnss-driver-overview"></a>GNSS 驱动程序概述


使用 GNSS 驱动程序设计指南，了解如何实现**DeviceIoControl** GNSS 驱动程序的 Api，以便像 GNSS 适配器的高级别的操作系统组件 (HLOS) 可以访问所需的 GNSS 功能。

GNSS 功能可以通过 IHV 提供较低的电源成本的位置或提供更好的性能在需要时进行扩充。

新的 GNSS 驱动程序完全拥有和 Ihv，随在内核模式下运行任何 Microsoft 所有的代码。

**请注意**  Ihv 必须将筛选器驱动程序添加到 GNSS/位置堆栈。 筛选器驱动程序很难调试和维护中通常不建议这样。 除此之外，在将来，Microsoft 可能需要添加用于扩展功能并附加的筛选器驱动程序从 Ihv GNSS 设备堆栈中的筛选器驱动程序将使体系结构更复杂不必要地。

 

该驱动程序遵循功能的驱动程序的泛型 UMDF 2.0 模型 （用户模式驱动程序框架）。 无法使用 KMDF （内核模式驱动程序框架） 驱动程序，但当其返回给该平台不稳定的风险更高时，就越难以调试，并无法进行直接使用用户模式下 OS 组件，它们是强烈建议不要使用。
此设计指南假定你基本熟悉 UMDF 2.0 中，Windows 内核模式编程、 内核 I/O 管理、 电源管理和即插即用设备堆栈。

## <a name="related-topics"></a>相关主题
[GNSS 驱动程序要求](gnss-driver-requirements.md)  
[GNSS 驱动程序体系结构](gnss-driver-architecture.md)  



