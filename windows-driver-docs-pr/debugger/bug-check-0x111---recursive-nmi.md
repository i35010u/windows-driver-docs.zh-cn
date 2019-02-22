---
title: Bug 检查 0x111 RECURSIVE_NMI
description: RECURSIVE_NMI bug 检查具有 0x00000111 值。 此 bug 检查指示正在进行以前 NMI 时发生非屏蔽的中断 (NMI)。
ms.assetid: 1f275db1-ac79-4bd2-85c5-cb64342911d1
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
ms.openlocfilehash: b41e0ce55105ae1fcd1f00757d9c9caec5805319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526421"
---
# <a name="bug-check-0x111-recursivenmi"></a>Bug 检查 0x111:递归\_NMI


递归\_NMI bug 检查的值为 0x00000111。 此 bug 检查指示正在进行以前 NMI 时发生非屏蔽的中断 (NMI)。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

<a name="remarks"></a>备注
-------

此 bug 检查发生在系统管理中断 (SMI) 代码中，没有错误并且 SMI 中断 NMI 并启用中断。 然后执行将继续与 NMIs 启用，而另一个 NMI 中断正在进行中的 NMI。

 

 




