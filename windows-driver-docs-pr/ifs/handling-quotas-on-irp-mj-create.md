---
title: 处理 IRP_MJ_CREATE 上的配额
description: 处理 IRP_MJ_CREATE 上的配额
keywords:
- IRP_MJ_CREATE
- 配额 WDK 文件系统
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2566d41aa22d76b2c2b83735cf446e1bb131e0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814448"
---
# <a name="handling-quotas-on-irp_mj_create"></a>处理 IRP \_ MJ CREATE 的 \_ 配额


## <span id="ddk_handling_quotas_on_irp_mj_create_if"></span><span id="DDK_HANDLING_QUOTAS_ON_IRP_MJ_CREATE_IF"></span>


如果文件系统支持配额，还可以包含某些逻辑以获取配额信息。 文件系统可以采用的一种策略是获取有关 [**irp \_ MJ \_ CREATE**](./irp-mj-create.md) 的配额信息块，稍后将通过调度例程来检查和更新这些请求，这些请求会更改文件大小 (删除和写入操作，例如) 。

 

