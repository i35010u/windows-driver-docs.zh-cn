---
title: EFI_CHECKSIG_PROTOCOL.EfiCheckSignatureAndHash
description: EFI_CHECKSIG_PROTOCOL.EfiCheckSignatureAndHash
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42077f7b3f586d2f7759d3c3c55498f5bccc1f29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789111"
---
# <a name="efi_checksig_protocolefichecksignatureandhash"></a>EFI \_ CHECKSIG \_ 协议。EfiCheckSignatureAndHash


此函数根据设备上的 PK 验证 FFU 中的目录文件上的签名。 它还验证哈希表的哈希是否与目录文件中指定的哈希匹配。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS
(EFIAPI * EFI_CHECK_SIG_AND_HASH) (
  IN EFI_CHECKSIG_PROTOCOL *This,
  IN UINT8 *pbCatalogData,
  IN UINT32 cbCatalogData,
  IN UINT8 *pbHashTableData,
  IN UINT32 cbHashTableData
);
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] **EFI \_ CHECKSIG \_ 协议** 实例的指针中。

<a href="" id="pbcatalogdata"></a>*pbCatalogData*  
\[在 \] 指向目录数据的指针中。

<a href="" id="cbcatalogdata"></a>*cbCatalogData*  
\[\]大小（以字节为单位）。

<a href="" id="pbhashtabledata"></a>*pbHashTableData*  
\[在 \] 指向哈希表数据的指针中。

<a href="" id="cbhashtabledata"></a>*cbHashTableData*  
\[在 \] 哈希表数据的大小（以字节为单位）。

## <a name="return-value"></a>返回值


返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>函数已成功返回，且哈希表的目录签名有效。</p></td>
</tr>
<tr class="even">
<td><p>EFI_SECURITY_VIOLATION</p></td>
<td><p>目录签名或哈希表无效。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="even">
<td><p>EFI_NO_MAPPING</p></td>
<td><p>发生了内部错误;例如，未正确预配 PK。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


对此函数的调用是同步的。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




