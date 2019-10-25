---
title: 用户模式驱动程序日志记录
description: 为了获得更具可操作性的视频内存细分，Windows 显示驱动程序模型（WDDM）驱动程序必须公开 Microsoft Direct3D 资源与视频内存分配之间的关系。
ms.assetid: E850E148-821D-4544-A778-00B1B9D13964
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b12be227498c33ebbe103168480602fbba2fb397
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825408"
---
# <a name="span-iddisplayuser-mode_driver_loggingspanuser-mode-driver-logging"></a><span id="display.user-mode_driver_logging"></span>用户模式驱动程序日志记录


为了获得更具可操作性的视频内存细分，Windows 显示驱动程序模型（WDDM）驱动程序必须公开 Microsoft Direct3D 资源与视频内存分配之间的关系。 这可以从 Windows 8 开始，并引入了附加的用户模式驱动程序（UMD）日志记录接口。 将此信息添加到 Windows 事件跟踪（ETW）跟踪后，可以从 API 的角度查看视频内存分配。

|                                                                                   |                                  |
|-----------------------------------------------------------------------------------|----------------------------------|
| 最小 WDDM 版本                                                              | 1.2                              |
| 最大 Windows 版本                                                           | 8                                |
| 驱动程序实现-仅限完整图形和呈现                               | Mandatory                        |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **¦ UMDLogging** |

 

对于开发人员而言，UMD 日志记录可以阐明当前很难看到的内存开销，例如内部碎片或快速丢弃图面的影响。 它使 Microsoft 可以更好地与提供跟踪来分析性能问题的客户和合作伙伴合作。 具体而言，此功能可帮助克服调查与内存相关的性能问题的共同阻塞点：应用程序使用的工作集太大，但无法确定哪些 API 资源或调用导致了问题。

驱动程序必须通过实现 UMD ETW 接口来公开 Direct3D 资源与视频内存分配之间的关系。 除了记录事件之外，驱动程序还必须能够在任何时间点报告资源和分配之间的所有现有映射。

## <a name="span-idumd_driver_allocation_logging_ddispanspan-idumd_driver_allocation_logging_ddispanspan-idumd_driver_allocation_logging_ddispanumd-driver-allocation-logging-ddi"></a><span id="UMD_driver_allocation_logging_DDI"></span><span id="umd_driver_allocation_logging_ddi"></span><span id="UMD_DRIVER_ALLOCATION_LOGGING_DDI"></span>UMD 驱动程序分配日志记录 DDI


用户模式驱动程序分配日志记录设备驱动程序接口（DDI）在 Windows 事件跟踪（ETW）内核级别跟踪工具下提供事件，该功能显示了哪些 API 资源与 Microsoft DirectX 中的内核分配相关联图形内核子系统（Dxgkrnl）。

您可以使用 DDI 来发现内部内存碎片或表面迅速丢弃的影响，从而为 Microsoft 提供更好的跟踪信息，以帮助您确定性能问题，并帮助确定应用程序的资源或 API 调用的时间导致其使用太大的内存工作集。

使用 Umdprovider 标头中的这些函数、枚举和结构在用户模式显示驱动程序中记录事件：

-   [**UMDEtwLogMapAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwlogmapallocation)函数
-   [**UMDEtwLogUnmapAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwlogunmapallocation)函数
-   [**UMDEtwRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwregister)函数
-   [**UMDEtwUnregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwunregister)函数
-   [**UMDETW\_分配\_语义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/ne-umdprovider-_umdetw_allocation_semantic)枚举
-   [**UMDETW\_分配\_使用情况**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/ns-umdprovider-_umdetw_allocation_usage)结构

另请参阅 Umdetw 标头。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)，了解**¦ UMDLogging**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)，了解 Windows 8 中添加的功能。

 

 





