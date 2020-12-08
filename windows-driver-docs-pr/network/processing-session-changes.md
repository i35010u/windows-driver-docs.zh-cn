---
title: 处理会话更改
description: 处理会话更改
keywords:
- 用户交互 WDK 本机 802.11 IHV 扩展 DLL
- 会话更改 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e2a7618ae489add4a8691cfbd664081094b4ae2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822829"
---
# <a name="processing-session-changes"></a>处理会话更改




 

如果用户的会话更改状态，例如当用户登录或注销时，操作系统会通过调用 [*Dot11ExtIhvProcessSessionChange*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change) 函数向 IHV 扩展 DLL 通知有关会话更改的信息。 操作系统将会话更改的原因传递到 *uEventType* 参数。

如果 *uEventType* 参数设置为 WTS \_ session \_ 注销，则用户已从当前会话中注销。 在这种情况下，所有挂起的用户界面 (UI) 请求必须由 IHV 扩展 DLL 在内部取消，并且 DLL 必须为每个挂起的 UI 请求释放任何分配的资源。

 

 
