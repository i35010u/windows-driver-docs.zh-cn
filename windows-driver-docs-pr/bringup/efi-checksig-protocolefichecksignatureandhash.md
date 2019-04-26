---
title: EFI_CHECKSIG_PROTOCOL.EfiCheckSignatureAndHash
description: EFI_CHECKSIG_PROTOCOL.EfiCheckSignatureAndHash
ms.assetid: 7c6d1756-a3db-4754-9edb-af6ba1ecf65b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1957ac140db9ba79a90297385a8523e074fbbeec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328490"
---
# <a name="efichecksigprotocolefichecksignatureandhash"></a>EFI\_CHECKSIG\_PROTOCOL.EfiCheckSignatureAndHash


此函数验证针对目录文件中针对 PK FFU 在设备上的签名。 它还验证的哈希表的哈希匹配目录文件中指定的哈希。

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

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向的指针**EFI\_CHECKSIG\_协议**实例。

<a href="" id="pbcatalogdata"></a>*pbCatalogData*  
\[在\]指向目录数据的指针。

<a href="" id="cbcatalogdata"></a>*cbCatalogData*  
\[在\]目录数据，以字节为单位的大小。

<a href="" id="pbhashtabledata"></a>*pbHashTableData*  
\[在\]指向哈希表数据的指针。

<a href="" id="cbhashtabledata"></a>*cbHashTableData*  
\[在\]哈希表数据，以字节为单位的大小。

## <a name="return-value"></a>返回值


返回一个下面的状态代码。

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
<td><p>成功返回该函数和哈希表的目录签名有效。</p></td>
</tr>
<tr class="even">
<td><p>EFI_SECURITY_VIOLATION</p></td>
<td><p>目录签名或哈希表不是有效的。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="even">
<td><p>EFI_NO_MAPPING</p></td>
<td><p>出现内部错误则例如，PK 未正确设置。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


对此函数调用是同步的。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




