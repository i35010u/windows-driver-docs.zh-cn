---
title: Bug Check 0x1D9 HAL_IOMMU_INTERNAL_ERROR
description: HAL_IOMMU_INTERNAL_ERROR bug 检查具有 0x000001D9 值。 它指示 UcmUcsi 驱动程序遇到错误。
keywords:
- Bug Check 0x1D9 HAL_IOMMU_INTERNAL_ERROR
- HAL_IOMMU_INTERNAL_ERROR
ms.date: 01/14/2019
topic_type:
- apiref
api_name:
- HAL_IOMMU_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24eef8b8fec9836751aee69f6ea0b9b955837ead
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361601"
---
# <a name="bug-check-0x1d9-haliommuinternalerror"></a>Bug 检查 0x1D9：HAL\_IOMMU\_INTERNAL\_ERROR

HAL\_IOMMU\_内部\_错误 bug 检查的值为 0x000001D9。 它指示 HAL IOMMU 库中检测到内部错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 
## <a name="haliommuinternalerror-parameters"></a>HAL\_IOMMU\_内部\_错误参数

|参数|描述|
|-------- |---------- |
|1| 指示失败的操作。 请参阅下面的值。|
|2| 请参阅下面的值。 |
|3| 请参阅下面的值。 |
|4| 请参阅下面的值。 |

**失败的操作值**

```text
0x00 : Failed to delete IOMMU domain
     Parameter 2 - Status
     Parameter 3 - Pointer to the IOMMU domain object

0x01 : Failed to unmap pages from IOMMU domain
     Parameter 2 - Status
     Parameter 3 - Pointer to the IOMMU domain object
     Parameter 4 - Logical address

0x02 : Failed to leave IOMMU domain
     Parameter 2 - Status
     Parameter 3 - Pointer to the IOMMU domain object
```

## <a name="cause"></a>原因
-----

HAL IOMMU 库中检测到内部错误。

## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)
