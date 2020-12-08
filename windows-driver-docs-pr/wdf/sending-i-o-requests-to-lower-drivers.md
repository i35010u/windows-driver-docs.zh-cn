---
title: 将 I/O 请求发送到较低的驱动程序
description: 将 I/O 请求发送到较低的驱动程序
keywords:
- I/o 请求 WDK UMDF，更低的驱动程序
- 请求处理 WDK UMDF，更低的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5728e5e107efdc932945abea7025334d3dcda4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821159"
---
# <a name="sending-io-requests-to-lower-drivers"></a>将 I/O 请求发送到较低的驱动程序


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序收到无法完全处理的 i/o 请求时，驱动程序通常会将接收到的请求转发到堆栈中的下一个较低的驱动程序。 驱动程序调用 [**IWDFIoRequest：： Send**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send) 方法转发请求。 为了同步转发，驱动程序将 \_ \_ \_ \_ 在 *Flags* 参数中传递 WDF 请求发送选项同步标志。 否则，驱动程序会以异步方式转发请求。 在驱动程序转发请求之前，它应该注册一个完成例程。 有关详细信息，请参阅 [完成 I/o 请求](completing-i-o-requests.md)。

 

