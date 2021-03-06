---
title: MB 基于设备的重置和恢复跟踪
description: MB 基于设备的重置和恢复跟踪
keywords:
- MB 基于设备的重置和恢复、基于移动宽带设备的重置和恢复、移动宽带微型端口驱动程序基于设备的重置和恢复
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 9a831aa991ef958af6a6ea00f2cc2a8b474dff9b
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250513"
---
# <a name="mb-device-reset-and-recovery-rnr-trace"></a>MB 设备重置和恢复 (RnR) trace
## <a name="useful-keywordsregexp-for-filtering-traces"></a>用于筛选跟踪的有用关键字/regexp
- 尝试重置连接
- 当前 RnR 状态
- OnConnectionStateInfoChanged
- EvaluateAndTryHighImpactRnRMethod
- CWwanResetRecovery：： Trigger
- CWwanResetRecovery：： Initialize
- CWwanResetRecovery::OnNdisNotification
- CWwanResetRecovery::OnWwanNotification
- CWwanResetRecovery::OnInterfaceReArrival
- CWwanResetRecovery::OnInterfaceRemoval
- CWwanResetRecovery::fsmEventHandler:
- CWwanResetRecovery::OnWwanNotification
- CWwanResetRecovery::fsmEventHandler: 
- CWwanDeviceEnumerator::
- CWwanResetRecovery
- SET OID_WWAN_RADIO_STATE (e010103) ，RequestId 
- ： OID_WWAN_CONNECT (
- NH调度 WwanNotificationSourceMsm\WwanMsmEventTypeConnectionIStreamUpdated
- ]RouteManagement::BadConnectionState
- WNF_WCM_INTERFACE_CONNECTION_STATE
- WNF_PHN_CALL_STATUS
- L3ConnnectivityGood
- WaitL3ConnnectivityGood
- CONTEXT_STATE Resp (集) 
- 找到有效
- _ReadRnRPolicies
- 机会 Internet
- 接口上的活动探测结果代码

## <a name="investigation-tips"></a>调查提示

* 确保日志中包含必要的 ETW 提供程序：

  1. netsh 跟踪开始 wireless_dbg，预配保留 = 是
  2. 重现方案 
  3. netsh 跟踪停止
  4. 收集生成的文件并将其附加到 bug 
       
* 按照 [RnR 触发器准则](mb-device-based-reset-and-recovery.md#rnr-triggers) ，确定导致 RnR 触发器的情况。

