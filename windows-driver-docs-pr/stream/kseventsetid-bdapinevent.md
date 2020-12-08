---
title: KSEVENTSETID \_ BdaPinEvent
description: KSEVENTSETID \_ BdaPinEvent
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 538f6a51feeb5aa83de12ec77592d5742dbe76ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819971"
---
# <a name="kseventsetid_bdapinevent"></a>KSEVENTSETID \_ BdaPinEvent


## <span id="ddk_kseventsetid_bdapinevent_ks"></span><span id="DDK_KSEVENTSETID_BDAPINEVENT_KS"></span>


KSEVENTSETID \_ BdaPinEvent 是 BDA 引脚事件集。 它用于向筛选器或应用程序通知请求与特定 pin 相关的事件的通知。

可用事件如下：

<span id="KSEVENT_BDA_PIN_CONNECTED"></span><span id="ksevent_bda_pin_connected"></span>[**\_ \_ 已连接 KSEVENT BDA PIN \_**](ksevent-bda-pin-connected.md)  
当 pin 连接时发出通知。

<span id="KSEVENT_BDA_PIN_DISCONNECTED"></span><span id="ksevent_bda_pin_disconnected"></span>[**KSEVENT \_ BDA \_ PIN 已 \_ 断开连接**](ksevent-bda-pin-disconnected.md)  
Pin 断开连接时发出通知。

### <a name="comments"></a>注释

当这些事件发生时，网络提供程序筛选器使用此事件集注册与 pin 相关的事件的通知。

如果 BDA 微型驱动程序未定义此事件集，则在 **BdaCreatePin** 或 **BdaInitFilter** 函数创建 pin 时，bda 支持库将添加支持。

如果某个 BDA 微型驱动程序定义了其自己的此事件集的处理程序，则微型驱动程序负责向此事件集中的事件发出信号，以通知以前请求通知的筛选器或插件。

 

 





