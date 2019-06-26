---
title: 如何初始化 WPP 软件跟踪中的内核模式驱动程序
description: 如何初始化 WPP 软件跟踪中的内核模式驱动程序
ms.assetid: 739428e8-14ff-4435-80e6-35b5c3366c79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cc6ed940ea8a467639189aacb307103e800b975
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356520"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-kernel-mode-driver"></a>如何在内核模式驱动程序中初始化 WPP 软件跟踪？


您可以通过调用初始化 WPP 内核模式驱动程序中的跟踪[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏来初始化 WPP 软件跟踪。

若要避免错误，应调用[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))中的宏[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/storage/driverentry-of-ide-controller-minidriver)驱动程序的函数。

 

 





