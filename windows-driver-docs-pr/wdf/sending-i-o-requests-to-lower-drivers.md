---
title: 将 I/O 请求发送到较低的驱动程序
description: 将 I/O 请求发送到较低的驱动程序
ms.assetid: 89868b4d-e2c1-4f38-b81e-a96b8cff3e4f
keywords:
- I/o 请求 WDK UMDF，更低的驱动程序
- 请求处理 WDK UMDF，更低的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d6a8aa1ea791672a8ee4ad4f3828899550ac076
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845202"
---
# <a name="sending-io-requests-to-lower-drivers"></a>将 I/O 请求发送到较低的驱动程序


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当驱动程序收到无法完全处理的 i/o 请求时，驱动程序通常会将接收到的请求转发到堆栈中的下一个较低的驱动程序。 驱动程序调用[**IWDFIoRequest：： Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)方法转发请求。 若要同步转发，驱动程序将在*Flags*参数中\_SEND\_选项\_同步标志传递 WDF\_请求。 否则，驱动程序会以异步方式转发请求。 在驱动程序转发请求之前，它应该注册一个完成例程。 有关详细信息，请参阅[完成 I/o 请求](completing-i-o-requests.md)。

 

 





