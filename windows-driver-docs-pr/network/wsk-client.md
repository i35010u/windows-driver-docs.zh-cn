---
title: WSK_CLIENT
description: 本主题介绍 WSK 应用程序的 WSK_CLIENT 数据类型。
ms.assetid: 7958dbd6-eaa6-4be8-a3a0-b3433ced924b
keywords:
- WSK_CLIENT，WDK WSK_CLIENT 网络驱动程序
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 808516d580816214b854fa43878d07d195ec750a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379371"
---
# <a name="wskclient"></a>WSK_CLIENT

WSK_CLIENT 数据类型定义为其附加到 WSK 应用程序的 WSK 子系统的绑定上下文。

```c++
typedef PVOID PWSK_CLIENT;
```

**PWSK_CLIENT**  
内容**WSK_CLIENT**结构是不透明的 WSK 应用程序。

## <a name="remarks"></a>备注

当 WSK 程序调用[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)函数，WSK 子系统返回一个指针为 WSK 应用程序通过 WSK_CLIENT 结构*WskProviderNpi*参数。 WSK 子系统使用此结构来跟踪 WSK 应用程序和 WSK 子系统之间的绑定的状态。 WSK 应用程序将此指针作为参数传递给所有函数中[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch) ([WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)， [WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)，和[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect))。

有关详细信息，请参阅[Winsock 内核应用程序注册](registering-a-winsock-kernel-application.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | 在 Windows Vista 和更高版本的 Windows 操作系统中可用。 |
| Header | Wsk.h （包括 Wsk.h） |

## <a name="see-also"></a>请参阅

[WskCaptureProviderNPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)  
[WskControlClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)  
[WskSocket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)  
[WskSocketConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)  
[WSK_PROVIDER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch)

