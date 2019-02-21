---
title: WDTF 体系结构
description: WDTF 体系结构
ms.assetid: 8c110e97-6870-41f1-a4f3-4d44b2974c1a
keywords:
- Windows 设备测试框架 WDK，体系结构
- WDTF WDK，体系结构
- WDK WDTF 体系结构
- Windows 设备测试框架 WDK 组件
- WDTF WDK 组件
- 面向设备的目标对象 WDK WDTF
- 面向系统的目标对象 WDK WDTF
- 目标对象 WDK WDTF
- 设备 depot WDK WDTF
- 系统 depot WDK WDTF
- 简单数据评估语言 WDK WDTF
- SDEL WDK WDTF
- 代码模块 WDK WDTF
- 查询语言 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19a42d9fe8aac2fa34dd5628e6704223a321ed01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519689"
---
# <a name="wdtf-architecture"></a>WDTF 体系结构


若要了解 WDTF 的体系结构，应该先阅读[Windows 设备测试框架设计指南](wdtf-overview.md)。 最重要的概念是 WDTF 使用设备和系统，通过将每个到抽象化*目标*( [ **IWDTFTarget2** ](https://msdn.microsoft.com/library/windows/hardware/hh439367)接口)。 下图显示 WDTF 提供的核心对象模型。

![说明 wdtf 核心对象模型的关系图](images/wdtf-objectmodel.gif)

部分或全部以下 WDTF 对象和接口，可以使用你的方案：

<a href="" id="wdtf-aggregation-object"></a>WDTF 聚合对象  
WDTF 聚合对象 ([**IWDTF2**](https://msdn.microsoft.com/library/windows/hardware/ff539628)) 是整个框架的初始实例化点。 框架中的所有内容都必须通过此对象访问。

<a href="" id="systemdepot-property"></a>[**SystemDepot** ](https://msdn.microsoft.com/library/windows/hardware/hh406309)属性  
[ **SystemDepot** ](https://msdn.microsoft.com/library/windows/hardware/hh406309)属性 ([**IWDTFSystemDepot2**](https://msdn.microsoft.com/library/windows/hardware/hh439331)) 包含仅本地计算机，使用户能够通过[**ThisSystem** ](https://msdn.microsoft.com/library/windows/hardware/hh439354)属性。

<a href="" id="devicedepot-property"></a>[**DeviceDepot** ](https://msdn.microsoft.com/library/windows/hardware/hh406304)属性  
[ **DeviceDepot** ](https://msdn.microsoft.com/library/windows/hardware/hh406304)属性 ([**IWDTFDeviceDepot2**](https://msdn.microsoft.com/library/windows/hardware/hh406391)) 表示的计算机可用的所有设备的集合。 方案脚本可以查询 (具有[**查询**](https://msdn.microsoft.com/library/windows/hardware/hh439483)方法) **DeviceDepot**满足一个或多个指定条件的搜索字符串中使用的设备的属性[简单数据评估语言](simple-data-evaluation-language-overview.md)(SDEL)。 上图中所示**查询**返回的目标集合 ([**IWDTFTargets2**](https://msdn.microsoft.com/library/windows/hardware/hh439458))，满足条件。 此外， **DeviceDepot**属性具有[ **RootDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh406413)表示 （也是父级的所有实际存在的逻辑设备对象的属性名为*非虚拟*) 在计算机中的设备。

<a href="" id="iwdtftarget2"></a>[**IWDTFTarget2**](https://msdn.microsoft.com/library/windows/hardware/hh439367)  
[ **IWDTFTarget2** ](https://msdn.microsoft.com/library/windows/hardware/hh439367)接口表示*目标*的测试活动。 使用框架执行的所有活动都涉及在至少一个目标。 目标可以具有以下形式之一：

-   一个*设备类型目标*表示连接到计算机的硬件 （或软件） 设备。

-   一个*系统类型目标*表示作为一个整体的计算机。

目标包含描述的设备或计算机它们所表示的属性。

<a href="" id="iwdtftargets2"></a>[**IWDTFTargets2**](https://msdn.microsoft.com/library/windows/hardware/hh439458)  
[ **IWDTFTargets2** ](https://msdn.microsoft.com/library/windows/hardware/hh439458)集合接口表示的各个目标集合 ([**IWDTFTarget2**](https://msdn.microsoft.com/library/windows/hardware/hh439367))。 [ **IWDTFTargets2::Query** ](https://msdn.microsoft.com/library/windows/hardware/hh439483)方法可用于检索另一个集合，其中包含包含目标的子集。

### <a name="action-plug-ins"></a>操作插件

WDTF 包括一组接口和实现 ([**操作接口**](https://msdn.microsoft.com/library/windows/hardware/ff538355))，可以控制目标为你的测试方案中使用。 每个实现知道如何执行特定于目标的操作，例如启用和禁用或执行 I/O 操作。 你的脚本可以引用这些接口由其接口名称，而无需了解特定的实现，如下图所示。

![说明 target::getinterface 方法的关系图](images/wdtf-getinterface.gif)

有关这些接口的详细信息，请参阅[控制目标](controlling-targets.md)。

### <a name="simple-data-evaluation-language-sdel"></a>简单数据评估语言 (SDEL)

WDTF 包括一种简单的查询语言，简单数据评估语言 (SDEL)，类似于 XPath，它可用于简化收集基于属性或关系的目标的任务。 SDEL 使您能够定义所选内容约束基于每个目标和它们之间的关系的两个属性的窗体简要查询语句。 有关 SDEL 详细信息，请参阅[简单数据评估语言概述](simple-data-evaluation-language-overview.md)。

 

 




