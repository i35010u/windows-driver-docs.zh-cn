---
title: 默认分配器
description: 默认分配器
ms.assetid: ef61a33d-eabf-4449-8d11-cfd97aa2e403
keywords:
- 默认分配器 WDK 内核流式处理
- 系统内存分配器 WDK 内核流式处理
- 内存分配器 WDK 内核流式处理
- 多个目标接收器，WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909caddd024b17301ff0da74ffcf1f75aad3cd9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837716"
---
# <a name="default-allocators"></a>默认分配器





默认分配器为从系统内存传输数据并需要特定内存分配属性的设备驱动程序提供系统内存分配器。 使用默认分配器时，筛选器只需处理分配器要求请求。

如果使用默认分配器，则微型驱动程序必须将 KSALLOCATOR\_REQUIREMENTF\_SYSTEM\_MEMORY 标志置于相关[**KSALLOCATOR\_组帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)结构的**RequirementsFlags**成员中。 提交 IRP\_MJ\_CREATE 并且 create type 为 KSCREATE\_REQUEST\_分配器时，该筛选器通过调用[**KsCreateDefaultAllocator**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedefaultallocator)函数将 IRP 转发到默认分配器处理程序。 所有剩余处理都由默认分配器进行处理。

 

 




