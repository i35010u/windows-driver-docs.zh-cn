---
title: 如何初始化 WPP 软件跟踪在用户模式应用程序
description: 如何初始化 WPP 软件跟踪在用户模式应用程序
ms.assetid: 1f1ab873-a1c3-4915-af31-ab74c1898fcb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2382b292e274fbdbc9b1d059004391a62fcd2f41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358285"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-user-mode-application"></a>如何在用户模式应用程序中初始化 WPP 软件跟踪？


您可以通过调用初始化 WPP 跟踪在用户模式应用程序[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏来初始化 WPP 软件跟踪。

若要避免错误，应调用[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏在其中任何跟踪尝试以前已经在源代码中的点。

 

 





