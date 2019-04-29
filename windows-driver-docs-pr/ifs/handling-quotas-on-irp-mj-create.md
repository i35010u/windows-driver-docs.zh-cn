---
title: 处理 IRP_MJ_CREATE 上的配额
description: 处理 IRP_MJ_CREATE 上的配额
ms.assetid: 71cf5e78-c87a-48fe-ba0b-f5efe8166525
keywords:
- IRP_MJ_CREATE
- 配额 WDK 文件系统
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 162182ad651b4ab694eb11e9efb0f8f891937f4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370140"
---
# <a name="handling-quotas-on-irpmjcreate"></a>处理 IRP 的配额\_MJ\_创建


## <span id="ddk_handling_quotas_on_irp_mj_create_if"></span><span id="DDK_HANDLING_QUOTAS_ON_IRP_MJ_CREATE_IF"></span>


此外可以包含一些逻辑获取配额信息，如果文件系统支持配额。 可采用这样的文件系统的一个策略是有关获取的配额信息块[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)更高版本的处于选中状态，并更新的调度例程可以更改文件的大小其他 IRP 请求 （删除和写入操作，例如）。

 

 




