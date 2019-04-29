---
title: 默认分配器
description: 默认分配器
ms.assetid: ef61a33d-eabf-4449-8d11-cfd97aa2e403
keywords:
- 默认分配器 WDK 内核流式处理
- 系统内存分配器 WDK 内核流式处理
- 内存分配器 WDK 内核流式处理
- 多个目标接收器 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05aa025a46e2fa3f00e6b777bfdc846cfa244e75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374098"
---
# <a name="default-allocators"></a>默认分配器





默认分配器设备驱动程序的系统内存中的传输数据提供系统内存分配器，并且需要特定的内存分配属性。 使用时的默认分配器，筛选器仅需要处理的分配器要求请求。

如果使用默认分配器，微型驱动程序必须设置 KSALLOCATOR\_REQUIREMENTF\_系统\_中的内存标志**RequirementsFlags**的相关成员[ **KSALLOCATOR\_组帧**](https://msdn.microsoft.com/library/windows/hardware/ff560979)结构。 当 IRP\_MJ\_提交创建，创建类型为 KSCREATE\_请求\_分配器，此筛选器转发到的默认分配器处理 IRP 通过调用[ **KsCreateDefaultAllocator** ](https://msdn.microsoft.com/library/windows/hardware/ff561641)函数。 由默认分配器处理所有剩余的处理。

 

 




