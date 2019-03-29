---
title: Bug 检查 0x40 TARGET_MDL_TOO_SMALL
description: TARGET_MDL_TOO_SMALL bug 检查具有 0x00000040 值。 这表示一个驱动程序具有不正确使用 IoBuildPartialMdl。
ms.assetid: bd154c1f-6c74-424e-bc32-22c9a93efae5
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
ms.openlocfilehash: e8e1642b5a7b200f744f4a917cc795823b4a4fdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567333"
---
# <a name="bug-check-0x40-targetmdltoosmall"></a>Bug 检查 0x40：目标\_MDL\_过\_小


目标\_MDL\_过\_小 bug 检查的值为 0x00000040。 这表示具有不正确使用驱动程序**IoBuildPartialMdl**。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="targetmdltoosmall-parameters"></a>目标\_MDL\_过\_小参数


无

<a name="cause"></a>原因
-----

这是一个驱动程序 bug。 驱动程序已调用**IoBuildPartialMdl**函数并将其传递 MDL 映射源 MDL 的一部分，但 MDL 不足够大，以将整个请求的地址范围映射的目标。

<a name="resolution"></a>分辨率
----------

源和目标 MDLs 以及地址范围长度要映射有第一，第二，以及第四个参数**IoBuildPartialMdl**函数。 因此，对此特定函数的堆栈跟踪，就可能有助于在调试过程。 请确保你的代码正确计算要传递给此函数的地址范围长度的目标 MDL 所需大小。

 

 




