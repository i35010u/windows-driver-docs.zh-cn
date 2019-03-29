---
title: EFI_RNG_SERVICE_BINDING_PROTOCOL
description: 用于查找 RNG 服务提供的驱动程序，以及创建和销毁实例，以便多个驱动程序可以使用基础 RNG 服务。
ms.assetid: 3CAD0FD8-DD26-4D26-A9E9-4B2750985E00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ffb9e550304f102452a6ab2368548b04450310b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564831"
---
# <a name="efirngservicebindingprotocol"></a>EFI\_RNG\_SERVICE\_BINDING\_PROTOCOL


EFI\_RNG\_服务\_绑定\_使用协议来查找驱动程序，提供的随机数字生成 (RNG) 服务，还可以创建和销毁实例 EFI\_RNG\_协议，以便多个驱动程序可以使用基础 RNG 服务。

泛型 EFI\_服务\_绑定\_协议 2.5.8 和 10.6 UEFI 规范的部分中所述。 本部分提供特定于信息 EFI\_RNG\_服务\_绑定\_协议。

## <a name="guid"></a>GUID


```cpp
// {E417A4A2-0843-4619-BF11-5CE82AFCFC59}
#define EFI_RNG_SERVICE_BINDING_PROTOCOL_GUID \
  {0xe417a4a2, 0x0843, 0x4619, 0xbf, 0x11, 0x5c, 0xe8, 0x2a, 0xfc, 0xfc, 0x59};
```

## <a name="remarks"></a>备注


应用程序或驱动程序需要 RNG 服务可以使用一个协议处理程序服务，例如 EFI\_引导\_服务-&gt;LocateHandleBuffer()，搜索设备发布 EFI\_RNG\_服务\_绑定\_协议。 每个设备提供已发布的 EFI\_RNG\_服务\_绑定\_协议应支持 EFI\_RNG\_协议并使其可供使用。

在成功调用了 EFI\_RNG\_服务\_绑定\_协议。CreateChild() 函数，子 EFI\_RNG\_协议驱动程序实例已准备好进行使用。

应用程序终止执行，EFI 的每个成功调用之前\_RNG\_服务\_绑定\_协议。必须匹配 CreateChild() 函数通过调用 EFI\_RNG\_服务\_绑定\_协议。DestroyChild() 函数。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




