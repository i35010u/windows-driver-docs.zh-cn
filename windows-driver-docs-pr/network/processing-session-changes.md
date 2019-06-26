---
title: 处理会话更改
description: 处理会话更改
ms.assetid: 6684b27e-d2ba-4305-bbd2-27543c9ec0cf
keywords:
- 用户交互 WDK 本机 802.11 IHV 扩展 DLL
- 会话更改 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b1a2476e9b3146db66fff01cf4bafdc34e29e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385472"
---
# <a name="processing-session-changes"></a>处理会话更改




 

如果用户的会话状态发生变化，例如当用户登录或缩小，操作系统会通知 IHV 扩展 DLL，有关该会话通过调用来更改[ *Dot11ExtIhvProcessSessionChange* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_session_change)函数。 操作系统将传递到会话更改的原因*uEventType*参数。

如果*uEventType*参数设置为 WTS\_会话\_注销时，在用户登录基于当前会话。 在此情况下，IHV 扩展 dll，必须在内部取消所有挂起的用户界面 (UI) 请求和 DLL 必须释放任何已分配的资源，为每个挂起的用户界面请求。

 

 





