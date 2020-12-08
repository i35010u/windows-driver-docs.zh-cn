---
title: 暂停驱动程序堆栈
description: 暂停驱动程序堆栈
keywords:
- 驱动程序堆栈 WDK 网络，暂停
- 暂停驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b46275c16940a29661aff48a6d421f1b469b32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822865"
---
# <a name="pausing-a-driver-stack"></a>暂停驱动程序堆栈





NDIS 暂停驱动程序堆栈以完成操作，例如插入筛选器模块或添加绑定。 通常，驱动程序堆栈暂停操作按如下方式继续：

1.  NDIS 将 PnP 暂停事件发送到协议驱动程序。

    绑定进入暂停状态。 所有未完成的发送请求完成后，协议驱动程序将完成 PnP 事件。 绑定处于暂停状态。

2.  NDIS 暂停所有筛选器模块，从堆栈顶部开始，到微型端口驱动程序。

    在 NDIS 调用筛选器驱动程序的 [*FilterPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause) 函数后，筛选器模块将进入暂停状态。 当 NDIS 返回所有未完成的接收指示，并且所有未完成的发送操作完成后，筛选器模块将进入暂停状态。

3.  NDIS 暂停微型端口适配器。

    在 NDIS 调用微型端口驱动程序的 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause) 函数后，微型端口适配器将进入暂停状态。 当 NDIS 返回所有未完成的接收指示后，微型端口适配器将进入暂停状态。

**注意**  NDIS 驱动程序无法使暂停请求失败。 应记录发生的任何错误。

 

 

