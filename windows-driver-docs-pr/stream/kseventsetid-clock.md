---
title: KSEVENTSETID \_ 时钟
description: 客户端可以通过以下方式请求接收时钟的时钟状态事件通知：将这些事件注册到时钟的文件对象 KSEVENT \_ 时钟 \_ 间隔 \_ MARKKSEVENT \_ 时钟 \_ 位置 \_ MARKWhen 客户端提交 IOCTL \_ KS \_ ENABLE \_ 事件请求来注册事件通知，并将其提交为每个事件引用页面的 EventData 部分中所述的结构。
keywords:
- KSEVENTSETID_Clock 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENTSETID_Clock
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 898f9871254eb4a02498961b7fc7beec49a934a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815817"
---
# <a name="kseventsetid_clock"></a>KSEVENTSETID \_ 时钟


客户端可以通过使用时钟的文件对象注册这些事件，请求在时钟上通知时钟状态事件：

[**KSEVENT \_ 时钟 \_ 间隔 \_ 标记**](ksevent-clock-interval-mark.md)

[**KSEVENT \_ 时钟 \_ 位置 \_ 标记**](ksevent-clock-position-mark.md)

当客户端提交 IOCTL \_ KS \_ ENABLE \_ 事件请求来注册事件通知时，它将提交为数据缓冲区，该结构记录在每个事件引用页的 **EventData** 节中。

 

 





