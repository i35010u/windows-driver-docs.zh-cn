---
title: Bug 检查 0x1D8 UCMUCSI_FAILURE
description: UCMUCSI_FAILURE bug 检查具有 0x000001D8 值。 它指示 UCSI 类扩展程序遇到错误。
keywords:
- Bug 检查 0x1D8 UCMUCSI_FAILURE
- UCMUCSI_FAILURE
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- UCMUCSI_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d94bb37cec00f13f4bbe728d64b4df8fe7062cc9
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743506"
---
# <a name="bug-check-0x1d8-ucmucsifailure"></a>Bug 检查 0x1D8:UCMUCSI\_失败

UCMUCSI\_故障错误检查的值为 0x000001D8。 它指示 UCSI 类扩展遇到了错误。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。
 
## <a name="ucmucsifailure-parameters"></a>UCMUCSI\_失败参数

|参数|描述|
|-------- |---------- |
|1| 失败的类型。 值：**0x0** :UCSI 命令已超时，因为固件没有响应的命令的时间。 **0x1** :UCSI 命令执行失败，因为客户端驱动程序返回了失败或固件返回了错误代码。 |
|2| UCSI 命令值。 |
|3| 如果非零指针，指向其他信息 (使用`dt UcmUcsiCx!UCMUCSICX_TRIAGE`)。 |
|4| 保留。 |

## <a name="cause"></a>原因
-----

UcmUcsi 驱动程序遇到错误。 设置触发系统故障而不是 livedump 已找到驱动程序。

## <a name="resolution"></a>分辨率
-----

UCSI 命令通常没有响应 UCSI 固件和 UcmUcsiCx UCSI 命令超时或 UCSI 固件已指明响应由 UcmUcsiCx 发送关键 UCSI 命令中的错误时将失败。

运行`!rcdrkd.rcdrlogdump UcmUcsiCx`有关此失败的原因的详细信息。 

分析此 bug 检查的详细信息，请参阅此博客文章-[调试 UCSI 固件故障](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/Debugging-UCSI-firmware-failures/ba-p/283226)。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

