---
title: WSK_CLIENT
description: 本主题介绍 WSK 应用程序的 WSK_CLIENT 数据类型。
ms.assetid: 7958dbd6-eaa6-4be8-a3a0-b3433ced924b
keywords:
- WSK_CLIENT，WDK WSK_CLIENT 网络驱动程序
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec0e8ed2a558fe03437a27b67906aff42ffd79c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844358"
---
# <a name="wsk_client"></a>WSK_CLIENT

WSK_CLIENT 数据类型为 WSK 应用程序的附件定义 WSK 子系统的绑定上下文。

```c++
typedef PVOID PWSK_CLIENT;
```

**PWSK_CLIENT**  
**WSK_CLIENT**结构的内容在 WSK 应用程序中是不透明的。

## <a name="remarks"></a>备注

当 WSK 应用程序调用[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)函数时，WSK 子系统通过*WSK*参数返回指向 WSKPROVIDERNPI 应用程序的 WSK_CLIENT 结构的指针。 WSK 子系统使用此结构跟踪 WSK 应用程序与 WSK 子系统之间的绑定的状态。 WSK 应用程序将此指针作为参数传递给[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch) （[WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)、 [WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)和[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)）中的所有函数。

有关详细信息，请参阅[注册 Winsock 内核应用程序](registering-a-winsock-kernel-application.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | 在 Windows Vista 和更高版本的 Windows 操作系统中可用。 |
| 标头 | Wsk （包括 Wsk） |

## <a name="see-also"></a>另请参阅

[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)  
[WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)  
[WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)  
[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)  
[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)

