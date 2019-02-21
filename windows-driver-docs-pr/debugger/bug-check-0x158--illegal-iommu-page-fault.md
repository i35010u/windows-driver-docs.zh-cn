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
ms.openlocfilehash: 2f0e6ab0034db9e7e5e302f1f5591c105ddc37de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532957"
---
# <a name="bug-check-0x158-illegaliommupagefault"></a>Bug 检查 0x158:非法\_IOMMU\_页\_容错


非法\_IOMMU\_页\_故障错误检查的值为 0x00000158。 这表示 IOMMU 已为无效 ASID 传递页错误数据包。 这并不安全，因为 ASID 可能被重用。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="illegaliommupagefault-parameters"></a>非法\_IOMMU\_页\_错误参数


| 参数 | 描述                           |
|-----------|---------------------------------------|
| 1         | 无效的 ASID。                     |
| 2         | 正在使用当前 ASIDs 数量。 |
| 3         | 使用此 ASID 的过程。          |
| 4         | ASID 的引用计数。           |

 

 

 




