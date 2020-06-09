---
title: Bug 检查 0x1D3 WFP_INVALID_OPERATION
description: WFP_INVALID_OPERATION bug 检查的值为0x000001D3。
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
ms.openlocfilehash: 04fb86d17a3a4d0aa3d7655d04965151ca0e1db1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534832"
---
# <a name="bug-check-0x1d3-wfp_invalid_operation"></a>Bug 检查 0x1D3：WFP_INVALID_OPERATION 

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


WFP_INVALID_OPERATION bug 检查的值为0x000001D3。 这表明 Windows 筛选平台标注执行了无效操作。

## <a name="wfp_invalid_operation-parameters"></a>WFP \_ 无效 \_ 操作参数

参数 | 说明 
|---------|--------------|
1 | 错误检查的子类型。
2 | 保留
3 | 保留
4 | 保留

**参数1值**

 0x1：标注注入了多 NET_BUFFERS 入站的 NBL。

 2-保留。

 3-指向 NBL 的指针。

 4-已保留。


## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。

 




