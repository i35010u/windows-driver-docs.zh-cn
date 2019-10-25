---
title: 框架对象事件
description: 框架对象事件
ms.assetid: 1bccdd47-8ad6-4607-947f-18c5d2e03038
keywords:
- framework 对象 WDK KMDF，事件
- 事件 WDK KMDF
- 事件 WDK KMDF，框架对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d350d7572d7153399b3c4b2911c4ce7f9d545936
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843118"
---
# <a name="framework-object-events"></a>框架对象事件





某些框架对象可以生成事件。 基于框架的驱动程序可以注册以接收所有、部分或全部对象事件的通知。 若要注册事件，驱动程序提供了事件回调函数。 事件发生时，框架会调用回调函数。

例如，驱动程序可以为 i/o 队列注册[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调函数。 每当框架准备好从 i/o 队列中删除 i/o 请求并将其传递给驱动程序时，框架就会调用此回调函数。

 

 





