---
title: 重置 （意外删除） 步骤 15 到 20
description: 如下所述的步骤 15 到 20，重置 （惊讶-删除） 的步骤。 步骤对应于 UE 挂起检测和恢复流中所示的图表。
ms.assetid: E72714A9-9B06-4609-820C-F25DC6BC0696
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c088a442c80dde3ff8ddda872eac39e855c7af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540926"
---
# <a name="reset-surprise-remove-steps-15-20"></a>重置 （意外删除）： 步骤 15 到 20


如下所述的步骤 15 到 20，重置 （惊讶-删除） 的步骤。 步骤对应于关系图中所示[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)。

后重置恢复可以继续，总线将导致即插即用来生成意外删除 IRP。 当 NDIS 收到意外删除 IRP 时，它调用返回 WDI 意外删除即插即用事件回调。 WDI 会意外删除作为 WDI 命令转发到 LE、 LE 在其中返回挂起的 WDI 命令。 流的余下部分等同于总线 (例如，USB) 上实际设备意外的删除。

清除命令流到 LE 以便返回的资源。 在此状态下，LE 应触摸硬件。

| 步骤 | 操作                                                                                                                                                               |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 15   | NDIS 回调即插即用事件的意外删除。                                                                                                                   |
| 16   | WDI 回调 LE 意外删除。                                                                                                                           |
| 17   | LE 返回挂起的 WDI 命令。 LE 仅需要一个槽的未完成的 WDI 命令因为 WDI 序列化到 LE、 诊断和中止除外 WDI 命令。 |
| 18   | WDI 会忽略挂起 WDI 命令返回，因为它已返回原始的 NDIS 命令。                                                                    |
| 19   | LE 返回 WDI 意外删除。                                                                                                                                  |
| 20   | WDI 返回 NDIS 即插即用意外删除的回调。                                                                                                                  |

 

## <a name="related-topics"></a>相关主题


[UE 挂起检测： 步骤 1 至 14 日](wdi-ue-hang-detection--step-1-to-step-14.md)

[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






