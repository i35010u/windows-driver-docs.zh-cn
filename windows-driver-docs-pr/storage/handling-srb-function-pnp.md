---
title: 处理 SRB_FUNCTION_PNP
description: 处理 SRB_FUNCTION_PNP
ms.assetid: 25490320-8d6b-4c5a-a585-4f628ea72393
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77ed3adba063aad446afb0a47a36f6a798ff0b95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533517"
---
# <a name="handling-srbfunctionpnp"></a>处理 SRB\_函数\_PNP


端口驱动程序将发送 SCSI\_PNP\_请求\_微型端口驱动程序块请求，以通知的 Windows 即插即用和播放 (PnP) 事件影响到适配器连接的存储设备微型端口驱动程序。

这些请求只是表示通知即插即用事件发生和微型端口驱动程序不需要任何操作。 微型端口驱动程序可执行 （例如，例如禁用其硬件） 的即插即用请求的上下文中的实际工作，但不是需要执行此操作。

如果 SRB 的函数成员设置为 SRB\_函数\_PNP，SRB 是一种结构的类型 SCSI\_PNP\_请求\_阻止。

 

 




