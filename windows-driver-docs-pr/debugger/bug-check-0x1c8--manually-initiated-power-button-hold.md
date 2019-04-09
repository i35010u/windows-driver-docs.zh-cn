---
title: Bug 检查 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD
description: MANUALLY_INITIATED_POWER_BUTTON_HOLD bug 检查具有 0x000001CE 值。 系统已配置为在用户按住电源按钮时启动出现 bugcheck。
keywords:
- Bug 检查 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD
- MANUALLY_INITIATED_POWER_BUTTON_HOLD
ms.date: 09/24/2018
topic_type:
- apiref
api_name:
- MANUALLY_INITIATED_POWER_BUTTON_HOLD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2fabfaff787d5d0535e398bff4565d9d1311ea0
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239050"
---
# <a name="bug-check-0x1c8-manuallyinitiatedpowerbuttonhold"></a>Bug 检查 0x1C8：手动\_INITIATED\_电源\_按钮\_保存

手动\_INITIATED\_电源\_按钮\_保持状态的值为 0x000001C8。

系统已配置为当用户指定的时间长度的电源按钮时启动出现 bugcheck。  这是用来捕获转储时系统之后，将为与长时间的电源按钮保持硬重置诊断出现 bugcheck。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


请注意，而不是标准"蓝屏"显示此 bug 检查时，则有以下文本的黑色背景以及 %进度指示器显示：

"请发布的电源按钮。 我们只需几个更多秒，若要关闭的情况下。" 


## <a name="manuallyinitiatedpowerbuttonhold-parameters"></a>手动\_INITIATED\_电源\_按钮\_保留参数

在蓝色屏幕上显示以下参数。

参数 | 描述 
|---------|--------------|
1 | 以毫秒为单位的电源按钮被按下的时间。
2 | 指向 nt ！ _POP_POWER_BUTTON_TRIAGE_BLOCK。
3 | 保留。
4 | 保留。


 

 




