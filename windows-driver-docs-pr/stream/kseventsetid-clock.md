---
title: KSEVENTSETID\_时钟
description: 客户端可以请求通过时钟的文件对象 KSEVENT 中注册这些事件通知的上一个时钟的时钟状态事件\_时钟\_间隔\_MARKKSEVENT\_时钟\_位置\_MARKWhen 客户端将提交 IOCTL\_KS\_启用\_事件请求以便注册事件通知，它将提交如数据缓冲区中每个事件引用页的 EventData 部分所述的结构。
ms.assetid: a411f83a-0361-4db6-9617-7c8588739cb4
keywords:
- KSEVENTSETID_Clock 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENTSETID_Clock
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e892e52be7e9ded9798a25ba15cd425552e4477e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569438"
---
# <a name="kseventsetidclock"></a>KSEVENTSETID\_时钟


客户端可以请求通过时钟的文件对象中注册这些事件通知的上一个时钟的时钟状态事件：

[**KSEVENT\_CLOCK\_INTERVAL\_MARK**](ksevent-clock-interval-mark.md)

[**KSEVENT\_时钟\_位置\_标记**](ksevent-clock-position-mark.md)

当客户端提交 IOCTL\_KS\_启用\_事件请求以便注册事件通知，它将提交数据缓冲区中所述的结构如**EventData**部分中的每个事件参考页。

 

 





