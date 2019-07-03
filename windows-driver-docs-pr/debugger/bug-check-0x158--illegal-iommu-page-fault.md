---
title: Bug 检查 0x158 ILLEGAL_IOMMU_PAGE_FAULT
description: ILLEGAL_IOMMU_PAGE_FAULT bug 检查具有 0x00000158 值。 这表示 IOMMU 已为无效 ASID 传递页错误数据包。
ms.assetid: E26C9B67-A332-4AE9-9325-9A3378EC9B36
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
ms.openlocfilehash: f5d0bdd69e57650942996cf8971f09a4c00c3e37
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520033"
---
# <a name="bug-check-0x158-illegaliommupagefault"></a>Bug 检查 0x158：非法\_IOMMU\_页\_容错


非法\_IOMMU\_页\_故障错误检查的值为 0x00000158。 这表示 IOMMU 已为无效 ASID 传递页错误数据包。 这并不安全，因为 ASID 可能被重用。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="illegaliommupagefault-parameters"></a>非法\_IOMMU\_页\_错误参数


| 参数 | 描述                           |
|-----------|---------------------------------------|
| 1         | 无效的 ASID。                     |
| 2         | 正在使用当前 ASIDs 数量。 |
| 3         | 使用此 ASID 的过程。          |
| 4         | ASID 的引用计数。           |

 

 

 




