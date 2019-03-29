---
title: KSEVENTSETID\_BdaPinEvent
description: KSEVENTSETID\_BdaPinEvent
ms.assetid: f81b9973-f4ae-4b39-a4e1-bbaff21c5d41
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb8e3320e00b1f4985615b20460447d15b85a1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565723"
---
# <a name="kseventsetidbdapinevent"></a>KSEVENTSETID\_BdaPinEvent


## <span id="ddk_kseventsetid_bdapinevent_ks"></span><span id="DDK_KSEVENTSETID_BDAPINEVENT_KS"></span>


KSEVENTSETID\_BdaPinEvent 是 BDA pin 事件集。 它用于通知筛选器或请求发送到特定的插针相关的事件通知的应用程序。

都可以与以下事件：

<span id="KSEVENT_BDA_PIN_CONNECTED"></span><span id="ksevent_bda_pin_connected"></span>[**KSEVENT\_BDA\_PIN\_CONNECTED**](ksevent-bda-pin-connected.md)  
Pin 将成为连接时通知。

<span id="KSEVENT_BDA_PIN_DISCONNECTED"></span><span id="ksevent_bda_pin_disconnected"></span>[**KSEVENT\_BDA\_PIN\_已断开连接**](ksevent-bda-pin-disconnected.md)  
Pin 断开连接时通知。

### <a name="comments"></a>备注

网络提供程序筛选器使用此设置来注册这些事件发生时与 pin 相关的事件通知的事件。

如果 BDA 微型驱动程序未定义此事件集，则 BDA 支持库添加了支持通过以下任一方法创建 pin 后**BdaCreatePin**或**BdaInitFilter**函数。

如果 BDA 微型驱动程序定义自己的处理程序为此事件集，微型驱动程序是负责信号中设置通知筛选器或插件的以前请求过通知此事件的事件。

 

 





