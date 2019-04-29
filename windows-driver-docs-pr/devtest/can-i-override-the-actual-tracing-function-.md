---
title: 可以重写实际跟踪函数
description: 可以重写实际跟踪函数
ms.assetid: 215e6fb6-a1f4-4188-a3aa-9688ce17d04b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0ea70b656d77ed08456cc59556b184210071968
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364725"
---
# <a name="can-i-override-the-actual-tracing-function"></a>是否可以重写实际跟踪函数？


是。 您可以执行此操作通过定义自定义 WPP\_TRACE 宏。 包括在内之前，必须定义此宏的版本[跟踪消息标头 (.tmh) 文件](trace-message-header-file.md)的源文件中您[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。

为举例说明如何定义自定义 WPP\_跟踪宏，请参阅[之前，可以我保留上一个错误代码调用 TraceMessage？](can-i-preserve-the-last-error-code-before-tracemessage-is-called-.md)。

 

 





