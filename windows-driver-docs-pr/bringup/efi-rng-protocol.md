---
title: EFI_RNG_PROTOCOL
description: EFI_RNG_PROTOCOL 用于从 EFI 驱动程序获取随机数生成 (RNG) 值。
ms.assetid: 927E2C40-973B-49AB-ACD5-2A3532827D74
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dfd1242d96af53444de42881f89b8410e1cb5a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527113"
---
# <a name="efirngprotocol"></a>EFI\_RNG\_协议


EFI\_RNG\_协议用于从 EFI 驱动程序获取随机数生成 (RNG) 值。

## <a name="syntax"></a>语法


```cpp
#define EFI_RNG_PROTOCOL_GUID \
  {0x3152bca5, 0xeade, 0x433d, 0x86, 0x2e, 0xc0, 0x1c, 0xdc, 0x29, 0x1f, 0x44};

typedef struct _EFI_RNG_PROTOCOL {
    EFI_RNG_GET_INFO    GetInfo;
    EFI_RNG_GET_RNG     GetRNG;
} EFI_RNG_PROTOCOL;
```

## <a name="members"></a>成员


<a href="" id="getinfo"></a>**GetInfo**  
返回有关 RNG 算法的信息，驱动程序支持。 有关详细信息，请参阅[EFI\_RNG\_协议。GetInfo](efi-rng-protocol-getinfo.md)。

<a href="" id="getrng"></a>**GetRNG**  
返回使用可选的 RNG 算法 RNG 值。 有关详细信息，请参阅[EFI\_RNG\_协议。GetRNG](efi-rng-protocol-getrng.md)。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




