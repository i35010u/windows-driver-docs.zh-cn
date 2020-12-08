---
title: 在通知通道两端实现的接口
description: 在通知通道两端实现的接口
keywords:
- 后台处理程序通知 WDK 打印，频道
- 打印后台处理程序通知 WDK，通道
- 通知通道 WDK 打印后台处理程序
- 频道通知 WDK 打印后台处理程序
- 数据通道 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1932ca4f3fda0588397b1b6715e6a0ceea30e89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796697"
---
# <a name="interfaces-implemented-at-both-ends-of-the-notification-channel"></a>在通知通道两端实现的接口





下图显示了用于后台处理程序异步通知的 COM 接口。

![说明后台处理程序异步通知中使用的 com 接口的关系图](images/splnotarch.png)

图片左侧描绘了通知通道的发送端，以及后台处理程序实现的接口。 图片右侧描述了通知通道的侦听器端，以及由应用程序或打印组件实现的接口以及由后台处理程序的服务器端实现的接口。 发送方和侦听器实现了在虚线上方显示的接口。 后台处理程序实现了虚线下显示的接口和函数。

 

 




