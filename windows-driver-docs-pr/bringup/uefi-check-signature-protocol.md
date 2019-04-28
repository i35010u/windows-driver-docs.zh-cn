---
title: UEFI 检查签名协议
description: UEFI 检查签名协议
ms.assetid: 71df491f-c507-4ca4-831b-50ca95167fb3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0bbaf1dd52f10bccb68f234e32bc1071874716a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337388"
---
# <a name="uefi-check-signature-protocol"></a>UEFI 检查签名协议


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

检查签名协议使闪烁工具，用于验证 FFU 中的目录文件的签名和验证哈希表的哈希与目录文件中指定的哈希值相匹配。

**请注意**  将此文档的未来版本中提供有关 FFU 文件和闪烁工具的结构信息。

 

## <a name="efichecksigprotocol"></a>EFI\_CHECKSIG\_协议


本部分提供的详细的说明**EFI\_CHECKSIG\_协议**。

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

**协议的接口结构**

```cpp
struct _EFI_CHECKSIG_PROTOCOL {
  UINT32 Revision;
  EFI_CHECK_SIG_AND_HASH EfiCheckSignatureAndHash;
};
```

**成员**

<a href="" id="revision"></a>**修订版本**  
修订**EFI\_CHECKSIG\_协议**遵循。 所有未来的版本必须是向后兼容。 如果将来的版本不是向后兼容，必须使用不同的 GUID。

<a href="" id="efichecksignatureandhash"></a>**EfiCheckSignatureAndHash**  
验证签名和 FFU 目录文件的哈希。 请参阅[EFI\_CHECKSIG\_协议。EfiCheckSignatureAndHash](efi-checksig-protocolefichecksignatureandhash.md)

## <a name="requirements"></a>要求


**标头：** 用户生成
