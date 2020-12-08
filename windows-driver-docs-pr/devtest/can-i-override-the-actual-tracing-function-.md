---
title: 能否重写实际的跟踪函数
description: 能否重写实际的跟踪函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6856ede3a4adbcd1e510883e4840d1e72ff7daa4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791573"
---
# <a name="can-i-override-the-actual-tracing-function"></a>是否可以重写实际跟踪函数？


是的。 可以通过定义自定义 WPP 跟踪宏来实现此目的 \_ 。 必须先定义此宏的版本，然后才能在[跟踪提供程序](trace-provider.md)的源文件中包含[跟踪消息标头 ( tmh) 文件](trace-message-header-file.md)，例如内核模式驱动程序或用户模式应用程序。

有关如何定义自定义 WPP 跟踪宏的示例 \_ ，请参阅 [在调用 TraceMessage 之前是否可以保留最后一个错误的代码？](can-i-preserve-the-last-error-code-before-tracemessage-is-called-.md)。

 

 





