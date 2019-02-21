---
title: 如何初始化 WPP 软件跟踪在用户模式应用程序
description: 如何初始化 WPP 软件跟踪在用户模式应用程序
ms.assetid: 1f1ab873-a1c3-4915-af31-ab74c1898fcb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b31b7e087c76a0f1919e6238ad60c95f0ba5fbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542348"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-application"></a>如何初始化 WPP 软件跟踪在用户模式应用程序？


您可以通过调用初始化 WPP 跟踪在用户模式应用程序[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏来初始化 WPP 软件跟踪。

若要避免错误，应调用[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏在其中任何跟踪尝试以前已经在源代码中的点。

 

 





