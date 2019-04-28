---
title: 如何初始化 WPP 软件跟踪中的内核模式驱动程序
description: 如何初始化 WPP 软件跟踪中的内核模式驱动程序
ms.assetid: 739428e8-14ff-4435-80e6-35b5c3366c79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358775b6a920a2c870eadaf38b9a58d37a8f6320
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329923"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-kernel-mode-driver"></a>如何在内核模式驱动程序中初始化 WPP 软件跟踪？


您可以通过调用初始化 WPP 内核模式驱动程序中的跟踪[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏来初始化 WPP 软件跟踪。

若要避免错误，应调用[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)中的宏[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552644)驱动程序的函数。

 

 





