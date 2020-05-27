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
ms.openlocfilehash: 36220da276f7c0a7ec79d05a3e30978d1715f990
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851483"
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
[**！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。

 




