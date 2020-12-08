---
title: WSK_CLIENT
description: 本主题介绍 WSK 应用程序的 WSK_CLIENT 数据类型。
keywords:
- WSK_CLIENT，WDK WSK_CLIENT 网络驱动程序
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b210b1c7fa620cde6aa112b36267397d546658
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813623"
---
# <a name="wsk_client"></a>WSK_CLIENT

WSK_CLIENT 数据类型为 WSK 应用程序的附件定义 WSK 子系统的绑定上下文。

```c++
typedef PVOID PWSK_CLIENT;
```

**PWSK_CLIENT**  
**WSK_CLIENT** 结构的内容对于 WSK 应用程序是不透明的。

## <a name="remarks"></a>备注

当 WSK 应用程序调用 [WskCaptureProviderNPI](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi) 函数时，WSK 子系统通过 *WskProviderNpi* 参数返回指向 WSK 应用程序的 WSK_CLIENT 结构的指针。 WSK 子系统使用此结构跟踪 WSK 应用程序与 WSK 子系统之间的绑定的状态。 WSK 应用程序将此指针作为参数传递给 [WSK_PROVIDER_DISPATCH](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch) ([WskControlClient](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)、 [WskSocket](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)和 [WskSocketConnect](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)) 中的所有函数。

有关详细信息，请参阅 [注册 Winsock 内核应用程序](registering-a-winsock-kernel-application.md)。

## <a name="requirements"></a>要求

**版本**：在 windows Vista 和更高版本的 windows 操作系统中可用。

**标头**： Wsk (包含 Wsk) 


## <a name="see-also"></a>请参阅

[WskCaptureProviderNPI](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)  
[WskControlClient](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)  
[WskSocket](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)  
[WskSocketConnect](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)  
[WSK_PROVIDER_DISPATCH](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)
