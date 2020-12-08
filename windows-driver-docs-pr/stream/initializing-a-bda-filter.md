---
title: 初始化 BDA 筛选器
description: 初始化 BDA 筛选器
keywords:
- BDA 微型驱动程序 WDK AVStream，筛选器初始化
- 正在初始化 BDA 筛选器
- 初始筛选器实例 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbb5de276b08c3cd0af4cc257c8bd22c86c8036e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806667"
---
# <a name="initializing-a-bda-filter"></a>初始化 BDA 筛选器





网络提供程序筛选器使用 BDA 设备初始筛选器描述符的创建调度例程在网络提供程序创建筛选器图时创建 BDA 设备的初始筛选器实例。 此初始筛选器描述符已设置为筛选器工厂，并在 BDA 设备启动时与 BDA 设备的 BDA 筛选器模板关联。 创建的初始筛选器实例应公开至少一个输入。 通常，初始筛选器实例将为初始筛选器描述符中的每个可能的输入插针公开输入插针，但不会公开任何输出插针。 有关详细信息，请参阅 [启动 BDA 微型驱动程序](starting-a-bda-minidriver.md) 和 [创建调度表](creating-dispatch-tables.md) 。

BDA 筛选器的 create 例程应为其筛选器对象分配内存，应为 filter 对象设置成员变量，然后应调用 [**BdaInitFilter**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter) 支持函数以初始化筛选器实例。 在此调用中，BDA 筛选器的 create 例程将传递指向用于创建初始筛选器的 [**KSFILTER**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter) 结构的指针，并将一个指针传递到 [**BDA \_ 筛选器 \_ 模板**](/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template) 结构的指针，该结构描述了初始筛选器实例的筛选器模板拓扑的可能性。

 

