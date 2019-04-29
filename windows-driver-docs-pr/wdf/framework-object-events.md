---
title: 框架对象事件
description: 框架对象事件
ms.assetid: 1bccdd47-8ad6-4607-947f-18c5d2e03038
keywords:
- framework 对象 WDK KMDF，事件
- 事件 WDK KMDF
- WDK KMDF，framework 对象的事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691ce0769e5cf35364a5e453ce02f4b2ed0326b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370992"
---
# <a name="framework-object-events"></a>框架对象事件





某些 framework 对象可以生成事件。 基于框架的驱动程序可以注册以接收通知的好处是，一些，或者没有任何对象的事件。 若要注册的事件，该驱动程序提供了一个事件的回调函数。 在事件发生时，框架将调用的回调函数。

例如，可以注册一个驱动程序[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757) I/O 队列的回调函数。 框架将调用此回调函数的每当 framework 准备好从 I/O 队列中删除的 I/O 请求并将其传送到驱动程序。

 

 





