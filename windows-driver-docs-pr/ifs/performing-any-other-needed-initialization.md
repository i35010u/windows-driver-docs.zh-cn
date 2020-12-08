---
title: 执行任何其他必需的初始化
description: 执行任何其他必需的初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e204e5399871ddc4b19324d2de5da2057c28aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832685"
---
# <a name="performing-any-other-needed-initialization"></a>执行任何其他必需的初始化


## <span id="ddk_performing_any_other_needed_initialization_if"></span><span id="DDK_PERFORMING_ANY_OTHER_NEEDED_INITIALIZATION_IF"></span>


注册 IRP 和快速 i/o 调度例程后，文件系统筛选器驱动程序的 **DriverEntry** 例程可以根据需要初始化其他全局驱动程序变量和数据结构。

 

 




