---
title: 处理 SRB_FUNCTION_PNP
description: 处理 SRB_FUNCTION_PNP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea486fc7c52a5fedc1770a61d35527a32988d79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835207"
---
# <a name="handling-srb_function_pnp"></a>处理 SRB \_ 函数 \_ PNP


端口驱动程序将 SCSI \_ PNP \_ 请求 \_ 块请求发送到微型端口驱动程序，以通知 Windows 即插即用 (PNP) 事件的微型端口驱动程序影响连接到该适配器的存储设备。

这些请求仅表示出现 PnP 事件的通知，并且无需微型端口驱动程序执行任何操作。 微型端口驱动程序可以在 PnP 请求的上下文中执行实际工作 (例如禁用其硬件，例如) ，但不需要执行此操作。

如果 SRB 的函数成员设置为 SRB \_ function \_ pnp，则 SRB 为类型为 "SCSI \_ PNP \_ 请求块" 的结构 \_ 。

 

 




