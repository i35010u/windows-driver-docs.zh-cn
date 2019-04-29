---
title: 用户模式驱动程序日志记录
description: 若要获取更具操作性的视频内存细分，Windows 显示驱动程序模型 (WDDM) 驱动程序必须公开 Microsoft Direct3D 资源和视频内存之间的关系。
ms.assetid: E850E148-821D-4544-A778-00B1B9D13964
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 291bc3072a934958d816240d2e563e0f90e14792
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359130"
---
# <a name="span-iddisplayuser-modedriverloggingspanuser-mode-driver-logging"></a><span id="display.user-mode_driver_logging"></span>用户模式驱动程序日志记录


若要获取更具操作性的视频内存细分，Windows 显示驱动程序模型 (WDDM) 驱动程序必须公开 Microsoft Direct3D 资源和视频内存之间的关系。 这可从 Windows 8 开始引入其他用户模式驱动程序 (UMD) 日志记录接口。 使用此信息添加到事件跟踪 Windows (ETW) 跟踪，它可能会看到从 API 的角度来看的视频内存分配。

|                                                                                   |                                  |
|-----------------------------------------------------------------------------------|----------------------------------|
| WDDM 的最低版本                                                              | 1.2                              |
| 最大 Windows 版本                                                           | 8                                |
| 驱动程序实现 — 仅完全图形和呈现                               | 强制                        |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **Device.Graphics¦UMDLogging** |

 

对于开发人员，UMD 日志记录可以明确目前很难看到的例如内部碎片或快速放弃曲面的影响的内存成本。 它可让 Microsoft 为了更好地与客户和合作伙伴提供的性能问题的分析跟踪的人员。 具体而言，此功能可帮助克服中调查与内存相关的性能问题的常见阻塞点： 应用程序正在使用太大工作集，但不能确定哪个 API 资源或调用导致了该问题。

该驱动程序必须通过实现 UMD ETW 接口公开的 Direct3D 资源和视频内存之间的关系。 除了记录事件，该驱动程序必须能够及时报告资源与分配任何时刻之间的所有现有映射。

## <a name="span-idumddriverallocationloggingddispanspan-idumddriverallocationloggingddispanspan-idumddriverallocationloggingddispanumd-driver-allocation-logging-ddi"></a><span id="UMD_driver_allocation_logging_DDI"></span><span id="umd_driver_allocation_logging_ddi"></span><span id="UMD_DRIVER_ALLOCATION_LOGGING_DDI"></span>日志记录 DDI UMD 驱动程序分配


用户模式驱动程序分配日志记录设备驱动程序接口 (DDI) 提供了在 Windows 事件跟踪 (ETW) 内核级别跟踪工具显示哪些 API 资源与 Microsoft DirectX 中的内核分配相关联的事件图形内核子系统 (Dxgkrnl.sys)。

若要发现内部内存碎片或应用层协议迅速被放弃的影响，以提供更好的 Microsoft 以帮助你识别性能问题，并帮助确定当应用程序的资源或 API 调用的跟踪信息，可以使用 DDI导致它要使用的内存太大工作集。

使用这些函数、 枚举和结构 Umdprovider.h 标头中的用户模式显示驱动程序中记录事件：

-   [**UMDEtwLogMapAllocation**](https://msdn.microsoft.com/library/windows/hardware/jj542437) function
-   [**UMDEtwLogUnmapAllocation**](https://msdn.microsoft.com/library/windows/hardware/jj542438) function
-   [**UMDEtwRegister** ](https://msdn.microsoft.com/library/windows/hardware/jj542439)函数
-   [**UMDEtwUnregister** ](https://msdn.microsoft.com/library/windows/hardware/jj542440)函数
-   [**UMDETW\_分配\_SEMANTIC** ](https://msdn.microsoft.com/library/windows/hardware/jj542441)枚举
-   [**UMDETW\_分配\_用法**](https://msdn.microsoft.com/library/windows/hardware/jj542442)结构

另请参阅 Umdetw.h 标头。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...UMDLogging**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





