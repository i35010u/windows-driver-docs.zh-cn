---
title: 在混合系统中使用跨适配器资源
description: Windows 显示器驱动程序模型 (WDDM) 驱动程序可以支持跨适配器资源集成的 GPU 和是分立的 GPU 之间的共享位置的混合系统。
ms.assetid: ECBB0AA7-50C2-41C8-9DC6-6EEFC5CEEB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea3970fae802be698797d295a53192fae0c02b3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373572"
---
# <a name="span-iddisplayusingcross-adapterresourcesinahybridsystemspanusing-cross-adapter-resources-in-a-hybrid-system"></a><span id="display.using_cross-adapter_resources_in_a_hybrid_system"></span>在混合系统中使用跨适配器资源


从 Windows 8.1 中，可以支持 Windows 显示驱动程序模型 (WDDM) 驱动程序*混合系统*，其中*跨适配器资源*集成的 GPU 和是分立的 GPU，之间共享和应用程序可以运行任一 GPU，具体取决于应用程序的需求上。 操作系统和驱动程序一起确定应用程序的运行在 GPU。

显示微型端口驱动程序应通过设置表达对跨适配器资源的支持**CrossAdapterResource**的成员[ **DXGK\_VIDMMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)结构。

驱动程序根据分配的类型以不同方式获取的信息。 如果分配是传统的全屏幕主数据库，用户模式显示驱动程序获取创建主数据库，如主标志、 视频存在网络 (VidPN) 源 ID、 刷新频率和旋转时通常提供的信息信息。 但是，如果分配是直接翻转主，跨适配器分配无法用作为主要副本，但用户模式显示驱动程序不会获得创建主数据库时提供的常用信息。 此外，在这种情况下离散的用户模式显示驱动程序接收主数据库的相关信息，但不是应验证它。 集成的驱动程序不会接收指示它是主键的信息。

这些后续主题提供有关驱动程序实现的混合系统的更多详细信息：

-   [正在验证混合系统配置](validating-a-hybrid-system-configuration.md)
-   [使用跨适配器资源是分立的 GPU 上呈现](rendering-on-a-discrete-gpu-using-cross-adapter-resources.md)
-   [混合系统 DDI](hybrid-system-ddi.md)

## <a name="span-iddefinitionofahybridsystemspanspan-iddefinitionofahybridsystemspandefinition-and-properties-of-a-hybrid-system"></a><span id="definition_of_a_hybrid_system"></span><span id="DEFINITION_OF_A_HYBRID_SYSTEM"></span>定义和混合系统属性：


-   系统包含单个集成的 GPU 和单个分立的 GPU:*集成 GPU*已集成到 CPU 芯片集和输出到如 LCD 面板集成的显示面板。
    *分立的 GPU*通常是连接到通过如 PCI 总线母板芯片集北部桥的可移动数据卡。
-   分立的 GPU 具有比集成 GPU 的明显更高性能。
-   分立的 GPU 是纯渲染设备，并没有显示输出连接到它。
-   Gpu 以物理方式括在同一机架中，既无法连接或断开连接时计算机运行的分立的 GPU。
-   安装新的驱动程序时，运行开机自检 (POST) 例程，或显示适配器是启用还是禁用状态时，操作系统检测到混合系统的配置。

## <a name="span-iddefinitionofacrossadapterresourcespanspan-iddefinitionofacrossadapterresourcespandefinition-and-properties-of-a-cross-adapter-resource"></a><span id="definition_of_a_cross_adapter_resource"></span><span id="DEFINITION_OF_A_CROSS_ADAPTER_RESOURCE"></span>定义和跨适配器资源的属性：


-   仅从 Windows 8.1 开始，提供跨适配器资源。
-   它可以是分页-仅对 aperture GPU 内存段。
-   它被分配为共享资源。
-   它有一个分配，以线性格式。
-   它具有 128 个字节的标准音调对齐方式 (由**D3DKMT\_跨\_适配器\_资源\_间距\_对齐**常量)。
-   它具有 4 行的标准高度对齐方式 (由**D3DKMT\_跨\_适配器\_资源\_高度\_对齐**常量)。
-   其内存起始地址与一个页边界对齐。
-   它可能会显示微型端口驱动程序作为从内核模式的标准分配中创建，然后由用户模式显示驱动程序更高版本打开。
-   它可能会创建用户模式显示驱动程序。

 

 





