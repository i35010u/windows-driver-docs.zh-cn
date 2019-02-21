---
title: 这两个点的通知通道实现的接口
description: 这两个点的通知通道实现的接口
ms.assetid: cc6f1b06-c185-4915-a212-d0b3a2702d5d
keywords:
- 后台处理程序通知 WDK 打印，通道
- 打印后台处理程序通知 WDK、 通道
- 通知通道 WDK 打印后台处理程序
- 通道通知 WDK 打印后台处理程序
- 数据通道 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf6e5128be561a2643635bfe428e9431a6f20b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524966"
---
# <a name="interfaces-implemented-at-both-ends-of-the-notification-channel"></a>这两个点的通知通道实现的接口





下图显示使用 COM 接口，在后台处理程序异步通知。

![说明在后台处理程序异步通知中使用的 com 接口的关系图](images/splnotarch.png)

左侧和右侧的图描绘了发件人结束的通知通道，以及后台处理程序实现的接口。 图片的右侧描绘了在侦听器端的通知通道，以及由应用程序或打印组件，而这些实现的后台处理程序的服务器端实现的接口。 发送方和侦听器实现虚线如上所示的接口。 后台处理程序实现的接口和虚线如下所示的函数。

 

 




