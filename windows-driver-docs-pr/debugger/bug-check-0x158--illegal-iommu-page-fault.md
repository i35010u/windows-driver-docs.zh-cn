---
title: Bug 检查 0x158 ILLEGAL_IOMMU_PAGE_FAULT
description: ILLEGAL_IOMMU_PAGE_FAULT bug 检查的值为0x00000158。 这表明 IOMMU 为无效的 ASID 传递了页面错误数据包。
keywords:
- Bug 检查 0x158 ILLEGAL_IOMMU_PAGE_FAULT
- ILLEGAL_IOMMU_PAGE_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ILLEGAL_IOMMU_PAGE_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 915ee9a4dd010ab63c213a61a45bd69380ebe702
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820967"
---
# <a name="bug-check-0x158-illegal_iommu_page_fault"></a>Bug 检查0x158：非法的 \_ IOMMU \_ 页面 \_ 错误


"非法 \_ IOMMU \_ 页 \_ 错误检查" 的值为0x00000158。 这表明 IOMMU 为无效的 ASID 传递了页面错误数据包。 这是不安全的，因为 ASID 可能已经被重复使用。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="illegal_iommu_page_fault-parameters"></a>非法的 \_ IOMMU \_ 页面 \_ 错误参数


| 参数 | 描述                           |
|-----------|---------------------------------------|
| 1         | 无效的 ASID。                     |
| 2         | 当前正在使用的 ASIDs 的数目。 |
| 3         | 使用此 ASID 的进程。          |
| 4         | ASID 的引用计数。           |

 

 

 




