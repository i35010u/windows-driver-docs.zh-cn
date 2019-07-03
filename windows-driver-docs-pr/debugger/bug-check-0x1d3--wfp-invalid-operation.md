---
title: Bug 检查 0x1D3 WFP_INVALID_OPERATION
description: WFP_INVALID_OPERATION bug 检查具有 0x000001D3 值。
keywords:
- Bug 检查 0x1D3 WFP_INVALID_OPERATION
- WFP_INVALID_OPERATION
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WFP_INVALID_OPERATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3695721b4260957408313cbf1f7460755b8a4371
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519658"
---
# <a name="bug-check-bug-check-0x1d3-wfpinvalidoperation"></a>Bug 检查 Bug 检查 0x1D3:WFP_INVALID_OPERATION 

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


WFP_INVALID_OPERATION bug 检查具有 0x000001D3 值。 这指示 Windows 筛选平台标注执行无效操作。

## <a name="wfpinvalidoperation-parameters"></a>WFP\_无效\_操作参数

参数 | 描述 
|---------|--------------|
1 | 检测的错误子类型。
2 | 保留
3 | 保留
4 | 保留


**参数 1 的值**

 0x1:标注注入与多个 NET_BUFFERS NBL 入站。

  2-保留。

  3-NBL 指向的指针。

  4-保留。


## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。

 




