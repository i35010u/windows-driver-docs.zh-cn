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
ms.openlocfilehash: 3f41801439af005811faad1a10ec1c231e7e9e7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384458"
---
# <a name="framework-object-events"></a>框架对象事件





某些 framework 对象可以生成事件。 基于框架的驱动程序可以注册以接收通知的好处是，一些，或者没有任何对象的事件。 若要注册的事件，该驱动程序提供了一个事件的回调函数。 在事件发生时，框架将调用的回调函数。

例如，可以注册一个驱动程序[ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) I/O 队列的回调函数。 框架将调用此回调函数的每当 framework 准备好从 I/O 队列中删除的 I/O 请求并将其传送到驱动程序。

 

 





