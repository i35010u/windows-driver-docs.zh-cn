---
title: 处理 IRP_MJ_CREATE 上的配额
description: 处理 IRP_MJ_CREATE 上的配额
ms.assetid: 71cf5e78-c87a-48fe-ba0b-f5efe8166525
keywords:
- IRP_MJ_CREATE
- 配额 WDK 文件系统
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28b7f2e1cfe7181d4ce9f11f7e947d539905a56e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063348"
---
# <a name="handling-quotas-on-irp_mj_create"></a>处理 IRP \_ MJ CREATE 的 \_ 配额


## <span id="ddk_handling_quotas_on_irp_mj_create_if"></span><span id="DDK_HANDLING_QUOTAS_ON_IRP_MJ_CREATE_IF"></span>


如果文件系统支持配额，还可以包含某些逻辑以获取配额信息。 文件系统可以采用的一种策略是获取有关 [**irp \_ MJ \_ CREATE**](./irp-mj-create.md) 的配额信息块，稍后将通过调度例程来检查和更新这些请求，这些请求会更改文件大小 (删除和写入操作，例如) 。

 

