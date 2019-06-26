---
title: 暂停驱动程序堆栈
description: 暂停驱动程序堆栈
ms.assetid: 6c6300e9-aea6-4da3-a91a-73db6ba8ff1f
keywords:
- 驱动程序堆栈 WDK 连接网络、 暂停
- 正在暂停驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ee227b67327fef41ab6503eb07bda8d9b54096f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382623"
---
# <a name="pausing-a-driver-stack"></a>暂停驱动程序堆栈





NDIS 暂停驱动程序堆栈，以完成操作，如插入筛选器模块或添加一个绑定。 一般情况下，驱动程序堆栈暂停操作的过程，如下所示：

1.  NDIS 即插即用暂停将事件发送到协议驱动程序。

    该绑定将进入暂停状态。 完成所有未完成发送请求后，协议驱动程序完成即插即用事件。 绑定是处于已暂停状态。

2.  NDIS 暂停所有筛选器模块在堆栈的顶部以开头和下微型端口驱动程序的进展情况。

    NDIS 调用筛选器驱动程序的后[ *FilterPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)函数，筛选器模块将进入暂停状态。 NDIS 返回所有未完成接收指标，以及所有未完成发送操作已完成后，筛选器模块将进入暂停状态。

3.  NDIS 暂停微型端口适配器。

    NDIS 调用微型端口驱动程序的后[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)函数，微型端口适配器进入暂停状态。 NDIS 返回所有未完成接收指示后，微型端口适配器进入暂停状态。

**请注意**  NDIS 驱动程序不能会暂停请求失败。 你应记录出现的任何错误。

 

 

 





