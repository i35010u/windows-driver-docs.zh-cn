---
title: UE 挂起检测和恢复流
description: 此图显示了 UE 挂起检测和重置流。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d37ea7c985bebc8e34c5469708cb99b77718cdd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821921"
---
# <a name="ue-hang-detection-and-recovery-flow"></a>UE 挂起检测和恢复流


此图显示了 UE 挂起检测和重置流。

![wdi 挂起检测和恢复流](images/wdi-hang-detection-recovery-flow.png)

此关系图包含主要阶段：

1.  挂起检测
2.  日志
3.  重置：意外删除处理

请务必记住，此功能可解决固件挂起。 它不会解决 IHV 驱动程序挂起。 仅当硬重新启动时，才能解决 IHV 驱动程序挂起。 驱动程序必须释放所有句柄和其他资源，然后才能将其卸载。 如果无法卸载该驱动程序，恢复将不起作用。

此流程图一般适用于所有 NDIS Oid 和对微型端口的回调。 在某些特殊情况下，如果 NDIS 或总线无法完全支持重置恢复，则重置恢复部分将不起作用。 两个示例事例是在微型端口初始化期间或在微型端口暂停操作期间。

## <a name="related-topics"></a>相关主题


[UE 挂起检测：步骤1-14](wdi-ue-hang-detection--step-1-to-step-14.md)

[重置 (意外删除) ：步骤15-20](wdi-reset--surprise-remove---steps-15-20.md)

 

 






