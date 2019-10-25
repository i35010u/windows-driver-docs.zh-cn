---
title: 在混合系统中使用跨适配器资源
description: Windows 显示驱动程序模型（WDDM）驱动程序可以支持混合系统，其中跨适配器资源在集成 GPU 和离散 GPU 之间共享。
ms.assetid: ECBB0AA7-50C2-41C8-9DC6-6EEFC5CEEB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f828150a97a283d8238b6f3c3dbea69828df42b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829278"
---
# <a name="span-iddisplayusing_cross-adapter_resources_in_a_hybrid_systemspanusing-cross-adapter-resources-in-a-hybrid-system"></a><span id="display.using_cross-adapter_resources_in_a_hybrid_system"></span>在混合系统中使用跨适配器资源


从 Windows 8.1 开始，Windows 显示驱动程序模型（WDDM）驱动程序可以支持*混合系统*，其中*跨适配器资源*在集成的 gpu 和离散 gpu 之间共享，并且应用程序可在任一 gpu 上运行，具体取决于应用程序的需求。 操作系统和驱动程序共同确定应用程序应运行的 GPU。

显示微型端口驱动程序应通过设置[**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)结构的**CrossAdapterResource**成员来对跨适配器资源提供支持。

驱动程序以不同的方式获取信息，具体取决于分配的类型。 如果分配是传统的全屏幕主副本，则用户模式显示驱动程序将获取创建主副本时通常提供的信息，例如主标志、视频显示网络（VidPN）源 ID、刷新率和旋转信息. 但是，如果分配是直接翻转的主副本，则可以将跨适配器分配用作主要副本，但用户模式显示驱动程序将不会获得创建主副本时所提供的常用信息。 此外，在这种情况下，离散用户模式显示驱动程序接收有关主副本的信息，但不应验证它。 集成驱动程序不会接收表明它是主要副本的信息。

以下主题提供了有关混合系统的驱动程序实现的更多详细信息：

-   [验证混合系统配置](validating-a-hybrid-system-configuration.md)
-   [使用跨适配器资源在离散 GPU 上呈现](rendering-on-a-discrete-gpu-using-cross-adapter-resources.md)
-   [混合系统 DDI](hybrid-system-ddi.md)

## <a name="span-iddefinition_of_a_hybrid_systemspanspan-iddefinition_of_a_hybrid_systemspandefinition-and-properties-of-a-hybrid-system"></a><span id="definition_of_a_hybrid_system"></span><span id="DEFINITION_OF_A_HYBRID_SYSTEM"></span>混合系统的定义和属性：


-   系统包含单个集成的 GPU 和单个离散 GPU：*集成的 gpu*集成到 CPU 芯片中，并输出到集成显示面板，如液晶屏面板。
    *离散 GPU*通常是一张可移动卡，它通过总线（如 PCI）连接到主板芯片的 "上桥"。
-   与集成 GPU 相比，离散 GPU 具有明显更高的性能。
-   离散 GPU 是一种仅呈现设备，无显示输出连接到该设备。
-   这两个 Gpu 都以物理方式包含在同一机架中，在计算机运行时，不能连接或断开离散 GPU。
-   当安装了新的驱动程序时，或者当启用或禁用显示适配器时，操作系统将检测混合系统的配置（当安装了新的驱动程序时）。

## <a name="span-iddefinition_of_a_cross_adapter_resourcespanspan-iddefinition_of_a_cross_adapter_resourcespandefinition-and-properties-of-a-cross-adapter-resource"></a><span id="definition_of_a_cross_adapter_resource"></span><span id="DEFINITION_OF_A_CROSS_ADAPTER_RESOURCE"></span>跨适配器资源的定义和属性：


-   跨适配器资源仅可从 Windows 8.1 开始。
-   它只能分页到口径 GPU 内存段。
-   它被分配为共享资源。
-   它只有一个线性格式的分配。
-   它的标准间距对齐方式为128字节（由**D3DKMT\_跨\_适配器定义\_资源\_跨度\_对齐**常量）。
-   它的标准高度对齐方式为4行（由**D3DKMT\_跨\_适配器定义\_资源\_高度\_对齐**常量）。
-   其内存起始地址与一页边界对齐。
-   它可以通过显示微型端口驱动程序作为内核模式的标准分配进行创建，然后由用户模式显示驱动程序打开。
-   它可由用户模式显示驱动程序创建。

 

 





