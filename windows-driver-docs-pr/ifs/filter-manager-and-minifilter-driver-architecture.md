---
title: 筛选器管理器和微筛选器驱动程序体系结构
description: 筛选器管理器和微筛选器驱动程序体系结构
ms.assetid: d3fde421-3475-4327-95cf-eaa520f5c132
keywords:
- 文件系统微筛选器驱动程序 WDK，体系结构
- 微筛选器驱动程序 WDK，体系结构
- 筛选器管理器 WDK 文件系统微筛选器
- 文件系统微筛选器驱动程序 WDK，筛选器管理器
- 微筛选器驱动程序 WDK，筛选器管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7ecc93c9a3dd9ae42b4b0fe444155b6a959fcf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524012"
---
# <a name="filter-manager-and-minifilter-driver-architecture"></a>筛选器管理器和微筛选器驱动程序体系结构


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


筛选器管理器是与传统的文件系统筛选器模型，并公开功能通常需要在文件系统筛选器驱动程序的内核模式驱动程序。 通过利用此功能，第三方开发人员可以编写微筛选器驱动程序，它是比旧的文件系统筛选器驱动程序更易于开发，从而生成更高质量、 更可靠的驱动程序同时缩短开发过程。

本部分包括：

[筛选器管理器的概念](filter-manager-concepts.md)

[筛选器管理器模型的优势](advantages-of-the-filter-manager-model.md)

[筛选器微筛选器驱动程序管理器的支持](filter-manager-support-for-minifilter-drivers.md)

[控制筛选器管理器操作](controlling-filter-manager-operation.md)

[开发和测试工具](development-and-testing-tools.md)

[对于移植旧筛选器驱动程序的指导原则](guidelines-for-porting-legacy-filter-drivers.md)

 

 


