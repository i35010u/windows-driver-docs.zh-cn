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
ms.openlocfilehash: 821537302427b9418495d68b38c262ba5aac2533
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367919"
---
# <a name="bug-check-0x111-recursivenmi"></a>Bug 检查 0x111：递归\_NMI


递归\_NMI bug 检查的值为 0x00000111。 此 bug 检查指示正在进行以前 NMI 时发生非屏蔽的中断 (NMI)。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


<a name="remarks"></a>备注
-------

此 bug 检查发生在系统管理中断 (SMI) 代码中，没有错误并且 SMI 中断 NMI 并启用中断。 然后执行将继续与 NMIs 启用，而另一个 NMI 中断正在进行中的 NMI。

 

 




