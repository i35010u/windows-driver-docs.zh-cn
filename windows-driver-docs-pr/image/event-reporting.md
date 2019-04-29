---
title: 事件报告
description: 事件报告
ms.assetid: 4c3ffa7e-d0b3-483c-9f6b-3fe8ae997cf0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efefb17f0a8f8ec846fb46bf837ada50810c1b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373135"
---
# <a name="event-reporting"></a>事件报告





WIA 体系结构使静态图像设备以在设备上的某些操作发生时通知 WIA 微型驱动程序。 例如，扫描程序可能按钮式，使用户可以启动直接从设备扫描其前面板上。 WIA 微型驱动程序必须通知此事件，以便它可以通知 WIA 服务。 所有正在运行的应用程序的已注册接收此事件会收到通知。 此外，如果应用程序已注册为最终触发此事件之前的事件，WIA 服务启动该应用程序。

WIA 体系结构支持中断事件，并轮询一次事件。 有关这些事件的详细信息，请参阅[WIA 驱动程序的事件支持](wia-driver-event-support.md)。

 

 




