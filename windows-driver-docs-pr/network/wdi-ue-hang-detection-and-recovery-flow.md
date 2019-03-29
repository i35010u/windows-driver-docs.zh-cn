---
title: UE 挂起检测和恢复流
description: 下图显示了 UE 挂起检测和重置流。
ms.assetid: 49B73223-91BA-4140-BB2B-8AB0CB355406
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f9ac505dfc6aa51305cc00e1b7ab0dbde515605
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567264"
---
# <a name="ue-hang-detection-and-recovery-flow"></a>UE 挂起检测和恢复流


下图显示了 UE 挂起检测和重置流。

![wdi 挂起检测和恢复流](images/wdi-hang-detection-recovery-flow.png)

在关系图的主要阶段包括：

1.  挂起检测
2.  日志
3.  重置： 意外删除处理

请务必记住，此功能来解决固件挂起。 它不能解决 IHV 驱动程序挂起。 仅可以通过硬重新启动解决 IHV 驱动程序挂起。 该驱动程序必须释放所有句柄和其他资源，才能卸载。 如果驱动程序不能卸载，恢复将不会工作。

此流关系图以一般方式适用于所有 NDIS Oid 和到微型端口的回调。 可能有特殊的情况下，如果 NDIS 或总线不能完全支持重置恢复，则重置恢复的恢复部分不起作用。 两个示例用例微型端口初始化期间或在微型端口过程会停止操作。

## <a name="related-topics"></a>相关主题


[UE 挂起检测： 步骤 1 至 14 日](wdi-ue-hang-detection--step-1-to-step-14.md)

[重置 （意外删除）： 步骤 15 到 20](wdi-reset--surprise-remove---steps-15-20.md)

 

 






