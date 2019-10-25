---
title: WDTF 体系结构
description: WDTF 体系结构
ms.assetid: 8c110e97-6870-41f1-a4f3-4d44b2974c1a
keywords:
- Windows 设备测试框架 WDK，体系结构
- WDTF WDK，体系结构
- 体系结构 WDK WDTF
- Windows 设备测试框架 WDK，组件
- WDTF WDK，组件
- 面向设备的目标对象 WDK WDTF
- 面向系统的目标对象 WDK WDTF
- 目标对象 WDK WDTF
- 设备仓库 WDK WDTF
- 系统仓库 WDK WDTF
- 简单数据评估语言 WDK WDTF
- SDEL WDK WDTF
- 代码模块 WDK WDTF
- 查询语言 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb616230159f4b975d6778dcb8c2521bf6840267
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844794"
---
# <a name="wdtf-architecture"></a>WDTF 体系结构


若要了解 WDTF 的体系结构，你应该首先阅读[Windows 设备测试框架设计指南](wdtf-overview.md)。 最重要的概念是 WDTF 使用设备和系统，方法是将每个设备和系统都抽象到一个*目标*中（一个[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)接口）。 下图显示了 WDTF 提供的核心对象模型。

![阐释 wdtf 核心对象模型的关系图](images/wdtf-objectmodel.gif)

你的方案可以使用以下部分或全部 WDTF 对象和接口：

<a href="" id="wdtf-aggregation-object"></a>WDTF 聚合对象  
WDTF 聚合对象（[**IWDTF2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)）是整个框架的初始实例化点。 必须通过此对象访问框架中的所有内容。

<a href="" id="systemdepot-property"></a>[**SystemDepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_systemdepot)属性  
[**SystemDepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_systemdepot)属性（[**IWDTFSystemDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfsystemdepot2)）仅包含本地计算机，你可以通过[**ThisSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfsystemdepot2-get_thissystem)属性访问该计算机。

<a href="" id="devicedepot-property"></a>[**DeviceDepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_devicedepot)属性  
[**DeviceDepot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtf2-get_devicedepot)属性（[**IWDTFDeviceDepot2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfdevicedepot2)）表示计算机上可用的所有设备的集合。 通过使用[简单的数据求值语言](simple-data-evaluation-language-overview.md)（SDEL），方案脚本可以查询（使用[**查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)方法）设备的**DeviceDepot**属性，该属性满足在搜索字符串中指定的一个或多个条件。 如上图所示， **Query**返回符合条件的目标（[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2)）的集合。 此外， **DeviceDepot**属性还具有一个[**RootDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfdevicedepot2-get_rootdevice)属性，该属性表示作为计算机中所有实际存在（也称为*非虚拟*）设备的父对象的逻辑设备对象。

<a href="" id="iwdtftarget2"></a>[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)  
[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)接口表示测试活动的*目标*。 您通过框架执行的所有活动都涉及至少一个目标。 目标可以具有以下形式之一：

-   *设备类型目标*表示连接到计算机的硬件（或软件）设备。

-   *系统类型目标*表示整个计算机。

目标包含描述它们所代表的设备或计算机的属性。

<a href="" id="iwdtftargets2"></a>[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2)  
[**IWDTFTargets2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2)集合接口表示各个目标的集合（[**IWDTFTarget2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2)）。 使用[**IWDTFTargets2：： Query**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)方法可以检索包含目标的子集的另一个集合。

### <a name="action-plug-ins"></a>操作插件

WDTF 包含一组可在测试方案中用于控制目标的接口和实现（[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)）。 每个实现都知道如何执行特定于目标的操作，例如启用和禁用，或者执行 i/o 操作。 您的脚本可以通过接口名称引用这些接口，而无需了解具体的实现方式，如下图所示。

![说明 target：： getinterface 方法的关系图](images/wdtf-getinterface.gif)

有关这些接口的详细信息，请参阅[控制目标](controlling-targets.md)。

### <a name="simple-data-evaluation-language-sdel"></a>简单数据计算语言（SDEL）

WDTF 包括简单的查询语言，简单的数据计算语言（SDEL），它类似于 XPath，并简化了基于属性或关系收集目标的任务。 通过 SDEL，您可以基于每个目标的属性和它们之间的关系，来构建简单的查询语句来定义选择约束。 有关 SDEL 的详细信息，请参阅[简单数据评估语言概述](simple-data-evaluation-language-overview.md)。

 

 




