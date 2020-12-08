---
title: EFI_RNG_SERVICE_BINDING_PROTOCOL
description: 用于查找驱动程序提供的 RNG 服务，以及创建和销毁实例，使多个驱动程序可以使用基础 RNG 服务。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57956b58888a1631848fb88564b0e1c492d507bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803399"
---
# <a name="efi_rng_service_binding_protocol"></a>EFI \_ RNG \_ 服务 \_ 绑定 \_ 协议


EFI \_ RNG \_ SERVICE \_ 绑定 \_ 协议用于定位由驱动程序提供) 的随机数字生成 (，以及创建和销毁 EFI RNG 协议的实例， \_ \_ 使多个驱动程序可以使用基础 RNG 服务。

\_ \_ \_ UEFI 规范的2.5.8 和10.6 部分介绍了一般 EFI 服务绑定协议。 本节提供特定于 EFI \_ RNG \_ SERVICE \_ 绑定 \_ 协议的信息。

## <a name="guid"></a>GUID


```cpp
// {E417A4A2-0843-4619-BF11-5CE82AFCFC59}
#define EFI_RNG_SERVICE_BINDING_PROTOCOL_GUID \
  {0xe417a4a2, 0x0843, 0x4619, 0xbf, 0x11, 0x5c, 0xe8, 0x2a, 0xfc, 0xfc, 0x59};
```

## <a name="remarks"></a>备注


需要 RNG services 的应用程序或驱动程序可以使用一种协议处理程序服务（例如 EFI \_ BOOT \_ services- &gt; LocateHandleBuffer ( # A1）来搜索发布 EFI \_ RNG \_ SERVICE \_ 绑定协议的设备 \_ 。 每个使用已发布的 EFI \_ RNG \_ SERVICE 绑定协议的设备 \_ \_ 都应支持 EFI \_ RNG \_ 协议，并使其可供使用。

成功调用 EFI \_ RNG \_ 服务 \_ 绑定 \_ 协议后。CreateChild ( # A1 函数，子 EFI \_ RNG \_ 协议驱动程序实例可供使用。

在应用程序终止执行之前，每次成功调用 EFI \_ RNG \_ SERVICE \_ 绑定 \_ 协议。CreateChild ( # A1 函数必须与对 EFI \_ RNG \_ 服务 \_ 绑定协议的调用匹配 \_ 。DestroyChild ( # A3 函数。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




