---
title: 如何实现在用户模式应用程序中初始化 WPP 软件跟踪
description: 如何实现在用户模式应用程序中初始化 WPP 软件跟踪
ms.assetid: 1f1ab873-a1c3-4915-af31-ab74c1898fcb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a24c9c98fa7fb37e05aef7b321ccadef5e737a0f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383187"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-application"></a>如何在用户模式应用程序中初始化 WPP 软件跟踪？


您可以通过调用 [wpp \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏初始化 wpp 软件跟踪，在用户模式应用程序中初始化 wpp 跟踪。

若要避免错误，应在源代码中的某个时间点调用 [WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏，但之前未进行任何跟踪尝试。

 

