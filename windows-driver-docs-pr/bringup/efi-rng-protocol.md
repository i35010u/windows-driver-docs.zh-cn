---
title: EFI_RNG_PROTOCOL
description: EFI_RNG_PROTOCOL 用于从 EFI 驱动程序 (RNG) 值获取随机数生成。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0697c3caa2d2e5d2dcde6de412ec23ce6675409
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789085"
---
# <a name="efi_rng_protocol"></a>EFI \_ RNG \_ 协议


EFI \_ RNG \_ 协议用于从 EFI 驱动程序获取随机数生成 (RNG) 值。

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
返回有关驱动程序支持的 RNG 算法的信息。 有关详细信息，请参阅 [EFI \_ RNG \_ 协议。GetInfo](efi-rng-protocol-getinfo.md)。

<a href="" id="getrng"></a>**GetRNG**  
使用可选的 RNG 算法返回 RNG 值。 有关详细信息，请参阅 [EFI \_ RNG \_ 协议。GetRNG](efi-rng-protocol-getrng.md)。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




