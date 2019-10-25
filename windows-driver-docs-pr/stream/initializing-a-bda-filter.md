---
title: 初始化 BDA 筛选器
description: 初始化 BDA 筛选器
ms.assetid: 716978f5-4bdd-4673-8c4a-14dc76947fba
keywords:
- BDA 微型驱动程序 WDK AVStream，筛选器初始化
- 正在初始化 BDA 筛选器
- 初始筛选器实例 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc6e63dcd775ce42df8f0ba7ca82dda00b1d26e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845576"
---
# <a name="initializing-a-bda-filter"></a>初始化 BDA 筛选器





网络提供程序筛选器使用 BDA 设备初始筛选器描述符的创建调度例程在网络提供程序创建筛选器图时创建 BDA 设备的初始筛选器实例。 此初始筛选器描述符已设置为筛选器工厂，并在 BDA 设备启动时与 BDA 设备的 BDA 筛选器模板关联。 创建的初始筛选器实例应公开至少一个输入。 通常，初始筛选器实例将为初始筛选器描述符中的每个可能的输入插针公开输入插针，但不会公开任何输出插针。 有关详细信息，请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)和[创建调度表](creating-dispatch-tables.md)。

BDA 筛选器的 create 例程应为其筛选器对象分配内存，应为 filter 对象设置成员变量，然后应调用[**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)支持函数以初始化筛选器实例。 在此调用中，BDA 筛选器的 create 例程会传递一个指向[**KSFILTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter)结构的指针，以创建初始筛选器，并将一个指针传递到[**BDA\_筛选器，\_模板**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)结构描述筛选器的可能初始筛选器实例的模板拓扑。

 

 




