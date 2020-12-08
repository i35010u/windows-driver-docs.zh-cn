---
title: 重置 (意外删除) 步骤15-20
description: 下面介绍了重置 (意外删除) （步骤15到20）的步骤。 这些步骤对应于 UE 挂起检测和恢复流中显示的关系图。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5050cf4bc1c14ecb6aefd22517a735db684e61ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822079"
---
# <a name="reset-surprise-remove-steps-15-20"></a>重置 (意外删除) ：步骤15-20


下面介绍了重置 (意外删除) （步骤15到20）的步骤。 这些步骤对应于 [UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)中显示的关系图。

重置恢复之后，总线会导致 PnP 生成意外删除 IRP。 当 NDIS 接收到意外删除 IRP 时，它将为 "意外删除 PnP 事件" 回调调用 WDI。 WDI 将意外删除作为 WDI 命令转发到 LE，其中 LE 返回挂起的 WDI 命令。 流的其余部分与在总线上的实际设备惊喜删除 (例如，USB) 相同。

清理命令流向了该 LE，以便于返回资源。 在此状态下，LE 不应触摸硬件。

| 步骤 | 操作                                                                                                                                                               |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 15   | NDIS 回调 PnP 事件以进行意外删除。                                                                                                                   |
| 16   | WDI 会回叫该 LE 以进行意外删除。                                                                                                                           |
| 17   | 该 LE 返回挂起的 WDI 命令。 该 LE 只需要槽来处理未完成的 WDI 命令，因为 WDI 将 WDI 命令序列化到 LE，诊断和中止除外。 |
| 18   | WDI 将忽略挂起的 WDI 命令的返回，因为它已返回原始 NDIS 命令。                                                                    |
| 19   | LE 返回 WDI 意外删除。                                                                                                                                  |
| 20   | WDI 返回用于意外删除的 NDIS PnP 回调。                                                                                                                  |

 

## <a name="related-topics"></a>相关主题


[UE 挂起检测：步骤1-14](wdi-ue-hang-detection--step-1-to-step-14.md)

[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






