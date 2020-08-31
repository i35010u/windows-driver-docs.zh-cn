---
title: 用户模式驱动程序日志记录
description: 为了获得更具可操作性的视频内存细分，Windows 显示驱动程序模型 (WDDM) 驱动程序必须公开 Microsoft Direct3D 资源与视频内存分配之间的关系。
ms.assetid: E850E148-821D-4544-A778-00B1B9D13964
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056f309748bc4669ca2506697726e1400382f257
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067156"
---
# <a name="span-iddisplayuser-mode_driver_loggingspanuser-mode-driver-logging"></a><span id="display.user-mode_driver_logging"></span>用户模式驱动程序日志记录


为了获得更具可操作性的视频内存细分，Windows 显示驱动程序模型 (WDDM) 驱动程序必须公开 Microsoft Direct3D 资源与视频内存分配之间的关系。 这是从 Windows 8 开始实现的，其中引入了附加的用户模式驱动程序 (UMD) 日志记录接口。 将此信息添加到 Windows (ETW) 跟踪的事件跟踪后，便可以从 API 角度查看视频内存分配。

**最小 WDDM 版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现-完整图形和仅呈现**：必需

** [WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试**： **Device. Graphics ¦ UMDLogging**


 

对于开发人员而言，UMD 日志记录可以阐明当前很难看到的内存开销，例如内部碎片或快速丢弃图面的影响。 它使 Microsoft 可以更好地与提供跟踪来分析性能问题的客户和合作伙伴合作。 具体而言，此功能可帮助克服调查与内存相关的性能问题的共同阻塞点：应用程序使用的工作集太大，但无法确定哪些 API 资源或调用导致了问题。

驱动程序必须通过实现 UMD ETW 接口来公开 Direct3D 资源与视频内存分配之间的关系。 除了记录事件之外，驱动程序还必须能够在任何时间点报告资源和分配之间的所有现有映射。

## <a name="span-idumd_driver_allocation_logging_ddispanspan-idumd_driver_allocation_logging_ddispanspan-idumd_driver_allocation_logging_ddispanumd-driver-allocation-logging-ddi"></a><span id="UMD_driver_allocation_logging_DDI"></span><span id="umd_driver_allocation_logging_ddi"></span><span id="UMD_DRIVER_ALLOCATION_LOGGING_DDI"></span>UMD 驱动程序分配日志记录 DDI


用户模式驱动程序分配日志记录设备驱动程序接口 (DDI) 在 Windows 的事件跟踪 (ETW 下提供事件) 内核级别跟踪工具，该工具显示哪些 API 资源与 Microsoft DirectX 图形内核子系统中的哪些内核分配 ( # A0) 关联。

您可以使用 DDI 来发现内部内存碎片或表面迅速被丢弃的影响，从而为 Microsoft 提供更好的跟踪信息，以帮助您确定性能问题，以及帮助确定应用程序的资源或 API 调用何时导致其使用过大的内存集。

使用 Umdprovider 标头中的这些函数、枚举和结构在用户模式显示驱动程序中记录事件：

-   [**UMDEtwLogMapAllocation**](/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwlogmapallocation) 函数
-   [**UMDEtwLogUnmapAllocation**](/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwlogunmapallocation) 函数
-   [**UMDEtwRegister**](/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwregister) 函数
-   [**UMDEtwUnregister**](/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwunregister) 函数
-   [**UMDETW \_分配 \_ 语义**](/windows-hardware/drivers/ddi/umdprovider/ne-umdprovider-_umdetw_allocation_semantic) 枚举
-   [**UMDETW \_分配 \_ 使用情况**](/windows-hardware/drivers/ddi/umdprovider/ns-umdprovider-_umdetw_allocation_usage) 结构

另请参阅 Umdetw 标头。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) ，了解 **¦ UMDLogging**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

 

