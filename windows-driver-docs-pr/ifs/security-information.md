---
title: 安全\_信息
description: 安全\_信息
ms.assetid: 28023f0f-62ae-407b-b81b-1c98499df9a2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee146129b5cadeeed2eb84597108ab6439b4c569
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840969"
---
# <a name="security_information"></a>安全\_信息


安全\_信息

``` syntax
typedef ULONG SECURITY_INFORMATION, *PSECURITY_INFORMATION;
```




Type SECURITY\_信息的值用于标识正在设置或查询的与对象相关的安全信息。 此安全信息包括：

-   对象的所有者

-   对象的主要组

-   对象的自由访问控制列表（DACL）

-   对象的系统 ACL （SACL）

安全信息的每一项都由一个位标志来指定。 以下值指定位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">含义</th>
<th align="left">访问</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置或查询对象的 DACL。</p>
<p>对于以下各项，将查询 DACL：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>对于以下各项，将设置 DACL：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要对 READ_CONTROL 的访问权限：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>需要对 WRITE_DAC 的访问权限：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置或查询对象的主要组标识符。</p>
<p>对于以下各项，将查询组标识符：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>对于以下各项，将设置组标识符：</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要对 READ_CONTROL 的访问权限：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>需要对 WRITE_OWNER 的访问权限：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置或查询对象的所有者标识符。</p>
<p>对于以下各项，将查询所有者标识符：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>对于以下各项，将设置所有者标识符：</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要对 READ_CONTROL 的访问权限：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>需要对 WRITE_OWNER 的访问权限：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置或查询对象的 SACL。</p>
<p>对于以下各项，将查询 SACL：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>对于以下各项，将设置 SACL：</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>所有情况下都需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PROCESS_TRUST_LABEL_SECURITY_INFORMATION</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


Wdm （包括 Wdm）

## <a name="related-topics"></a>相关主题


[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**SeQuerySecurityDescriptorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sequerysecuritydescriptorinfo)

[**SeSetSecurityDescriptorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sesetsecuritydescriptorinfo)

[**SeSetSecurityDescriptorInfoEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-sesetsecuritydescriptorinfoex)

[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)

[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)

 

 






