---
title: 如何实现在用户模式应用程序中初始化 WPP 软件跟踪
description: 如何实现在用户模式应用程序中初始化 WPP 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bab306d2652f96468e76d005c8be90491050c33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839131"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-application"></a>如何在用户模式应用程序中初始化 WPP 软件跟踪？


您可以通过调用 [wpp \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏初始化 wpp 软件跟踪，在用户模式应用程序中初始化 wpp 跟踪。

若要避免错误，应在源代码中的某个时间点调用 [WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏，但之前未进行任何跟踪尝试。

 

