---
title: UEFI 检查签名协议
description: UEFI 检查签名协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1669304667c7e65bbf09aec05e6c96980e7c8350
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783579"
---
# <a name="uefi-check-signature-protocol"></a>UEFI 检查签名协议


**注意**  本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

使用检查签名协议，闪烁工具可验证 FFU 中目录文件的签名，并验证哈希表的哈希是否与目录文件中指定的哈希匹配。

**注意**  此文档的未来版本中将提供有关 FFU 文件的结构和闪烁工具的信息。

 

## <a name="efi_checksig_protocol"></a>EFI \_ CHECKSIG \_ 协议


本部分提供 **EFI \_ CHECKSIG \_ 协议** 的详细说明。

**GUID**

```cpp
// {E52500C3-4BF4-41A5-9692-6DF73DBFB9FE}
#define EFI_CHECKSIG_PROTOCOL_GUID \
  { 0xe52500c3, 0x4bf4, 0x41a5, { 0x96, 0x92, 0x6d, 0xf7, 0x3d, 0xbf, 0xb9, 0xfe } }
```

**修订号**

```cpp
#define EFI_SIMPLE_WINPHONE_IO_PROTOCOL_REVISION   0x00000000
```

**协议接口结构**

```cpp
struct _EFI_CHECKSIG_PROTOCOL {
  UINT32 Revision;
  EFI_CHECK_SIG_AND_HASH EfiCheckSignatureAndHash;
};
```

**成员**

<a href="" id="revision"></a>**A01**  
**EFI \_ CHECKSIG \_ 协议** 遵循的修订版本。 所有将来的修订版都必须是向后兼容。 如果未来版本不是向后兼容的，则必须使用不同的 GUID。

<a href="" id="efichecksignatureandhash"></a>**EfiCheckSignatureAndHash**  
验证 FFU 目录文件的签名和哈希。 请参阅 [EFI \_ CHECKSIG \_ 协议。EfiCheckSignatureAndHash](efi-checksig-protocolefichecksignatureandhash.md)

## <a name="requirements"></a>要求


**标头：** 用户生成
