---
title: Bug 检查 0x40 TARGET_MDL_TOO_SMALL
description: TARGET_MDL_TOO_SMALL bug 检查的值为0x00000040。 这表明驱动程序未正确使用 IoBuildPartialMdl。
keywords:
- Bug 检查 0x40 TARGET_MDL_TOO_SMALL
- TARGET_MDL_TOO_SMALL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TARGET_MDL_TOO_SMALL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 946f571d75863dd2155436f5e6809f0a653e9a53
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787937"
---
# <a name="bug-check-0x40-target_mdl_too_small"></a>Bug 检查0x40：目标 \_ MDL \_ 太 \_ 小


目标 \_ MDL \_ 太 \_ 小 bug 检查的值为0x00000040。 这表明驱动程序未正确使用 **IoBuildPartialMdl**。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="target_mdl_too_small-parameters"></a>目标 \_ MDL \_ 太 \_ 小参数


无

<a name="cause"></a>原因
-----

这是驱动程序 bug。 驱动程序调用了 **IoBuildPartialMdl** 函数，并向其传递了一个 mdl 来映射源 MDL 的一部分，但目标 mdl 不够大，无法映射所请求的整个地址范围。

<a name="resolution"></a>解决方法
----------

源和目标 MDLs 以及要映射的地址范围长度是 **IoBuildPartialMdl** 函数的第一个、第二个和第四个参数。 因此，在调试过程中，对此特定函数执行堆栈跟踪可能会有所帮助。 确保你的代码正确计算要传递给此函数的地址范围长度的目标 MDL 所需的大小。

 

 




