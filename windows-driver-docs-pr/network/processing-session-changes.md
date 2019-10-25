---
title: 处理会话更改
description: 处理会话更改
ms.assetid: 6684b27e-d2ba-4305-bbd2-27543c9ec0cf
keywords:
- 用户交互 WDK 本机 802.11 IHV 扩展 DLL
- 会话更改 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ee43d8f4c908c250d1459513da592b14a0a4035
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843484"
---
# <a name="processing-session-changes"></a>处理会话更改




 

如果用户的会话更改状态，例如当用户登录或注销时，操作系统会通过调用[*Dot11ExtIhvProcessSessionChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change)函数向 IHV 扩展 DLL 通知有关会话更改的信息。 操作系统将会话更改的原因传递到*uEventType*参数。

如果*uEventType*参数设置为 WTS\_会话\_注销，则用户已从当前会话中注销。 在这种情况下，所有挂起的用户界面（UI）请求必须由 IHV 扩展 DLL 在内部取消，并且 DLL 必须为每个挂起的 UI 请求释放任何分配的资源。

 

 





