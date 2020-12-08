---
title: Bug 检查 0x159 HAL_ILLEGAL_IOMMU_PAGE_FAULT
description: HAL_ILLEGAL_IOMMU_PAGE_FAULT bug 检查的值为0x00000159。
keywords:
- Bug 检查 0x159 HAL_ILLEGAL_IOMMU_PAGE_FAULT
- HAL_ILLEGAL_IOMMU_PAGE_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HAL_ILLEGAL_IOMMU_PAGE_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0317a9546e6088ff063e08615826515712e53ec1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803991"
---
# <a name="bug-check-0x159-hal_illegal_iommu_page_fault"></a>Bug 检查0x159： HAL \_ 非法 \_ IOMMU \_ 页面 \_ 错误


HAL \_ 非法 \_ IOMMU \_ 页面 \_ 错误检查的值为0x00000159。 这表明 IOMMU 为正在释放的 ASID 提供了页错误。 驱动程序负责在此时间点之前完成任何即时请求，此错误检测表明系统中的驱动程序未执行此操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="hal_illegal_iommu_page_fault-parameters"></a>HAL \_ 非法 \_ IOMMU \_ 页面 \_ 错误参数


| 参数 | 描述                       |
|-----------|-----------------------------------|
| 1         | IOMMU 供应商消除歧义       |
| 2         | 指向错误数据包的指针           |
| 3         | 特定于供应商的错误数据包数据 |
| 4         | 特定于供应商的错误数据包数据 |

 

| 参数 | 描述                           |
|-----------|---------------------------------------|
| 1         | IOMMU 供应商歧义 = 0x3xxx。 |
| 2         | 状态                                |
| 3         | PASID                                 |
| 4         | DirectoryBase                         |

 

 

 




