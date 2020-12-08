---
title: Bug 检查 0x111 RECURSIVE_NMI
description: RECURSIVE_NMI bug 检查的值为0x00000111。 此 bug 检查表明在上一个 NMI 正在进行时， (NMI) 出现不可屏蔽中断。
keywords:
- Bug 检查 0x111 RECURSIVE_NMI
- RECURSIVE_NMI
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RECURSIVE_NMI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff03f554aae51c6d01bbc5d99aea6b6667b7d514
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790055"
---
# <a name="bug-check-0x111-recursive_nmi"></a>Bug 检查0x111：递归 \_ NMI


递归 \_ NMI bug 检查的值为0x00000111。 此 bug 检查表明在上一个 NMI 正在进行时， (NMI) 出现不可屏蔽中断。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


<a name="remarks"></a>备注
-------

如果系统管理中断 (SMI-S) 代码中存在错误，并且 SMI 中断 NMI 并启用中断，则会发生此 bug 检查。 然后，执行将继续，启用 NMIs，另一个 NMI 会中断正在进行的 NMI。

 

 




