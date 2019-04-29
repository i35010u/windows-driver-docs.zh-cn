---
title: 初始化 BDA 筛选器
description: 初始化 BDA 筛选器
ms.assetid: 716978f5-4bdd-4673-8c4a-14dc76947fba
keywords:
- BDA 微型驱动程序 WDK AVStream，筛选器初始化
- 初始化 BDA 筛选器
- 初始筛选器实例 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d76d72bb39ec6c47b50b9d6460f9d5abbc3b67a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360477"
---
# <a name="initializing-a-bda-filter"></a>初始化 BDA 筛选器





网络提供程序筛选器使用 BDA 设备的初始筛选器描述符创建调度例程时网络提供商创建一个筛选器图形创建 BDA 设备的初始筛选器实例。 此初始筛选器描述符设置为筛选器工厂，BDA 设备启动时与 BDA 设备 BDA 筛选器模板相关联。 创建初始的筛选器实例应公开至少一个输入。 通常情况下，初始的筛选器实例公开的初始筛选器描述符中每个可能的输入插针输入插针，但公开没有输出插针。 请参阅[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)并[创建调度表](creating-dispatch-tables.md)有关详细信息。

BDA 筛选器的创建例程应为其筛选器对象分配内存，应设置为该筛选器对象的成员变量，然后应调用[ **BdaInitFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556464)支持该函数以初始化筛选器实例中。 在此调用中，BDA 筛选器的创建常规传递一个指向[ **KSFILTER** ](https://msdn.microsoft.com/library/windows/hardware/ff562522)要创建的初始筛选器和一个指向结构[ **BDA\_筛选器\_模板**](https://msdn.microsoft.com/library/windows/hardware/ff556523)描述可能的初始的筛选器实例的筛选器的模板拓扑结构。

 

 




