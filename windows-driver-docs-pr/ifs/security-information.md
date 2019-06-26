---
title: 安全\_信息
description: 安全\_信息
ms.assetid: 28023f0f-62ae-407b-b81b-1c98499df9a2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d4ba2e9766057e6ed226a81c75d80f4b7027f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371336"
---
# <a name="securityinformation"></a>安全\_信息


安全\_信息

``` syntax
typedef ULONG SECURITY_INFORMATION, *PSECURITY_INFORMATION;
```




类型安全的值\_信息用于标识要设置或查询的对象相关的任何安全信息。 此安全信息包括：

-   对象所有者

-   对象的主要组

-   对象的自由访问控制列表 (DACL)

-   对象的系统 ACL (SACL)

每个项的安全信息被指定的位标志。 以下值指定位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
<th align="left">访问</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示对象的 DACL 正在设置或查询。</p>
<p>以下各项，查询 DACL:</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>以下各项设置 DACL:</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要为 READ_CONTROL 访问权限：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>需要 WRITE_DAC 访问的权限：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示该对象的主要组标识符正在设置或查询。</p>
<p>以下各项，查询组标识符：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>以下各项设置的组标识符：</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要为 READ_CONTROL 访问权限：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>需要为 WRITE_OWNER 访问权限：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示该对象的所有者标识符正在设置或查询。</p>
<p>以下各项，查询所有者标识符：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>以下各项设置所有者标识符：</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要为 READ_CONTROL 访问权限：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>需要为 WRITE_OWNER 访问权限：</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示对象的 SACL 正在设置或查询。</p>
<p>以下各项，SACL 被查询：</p>
<p>IRP_MJ_QUERY_SECURITY</p>
<p>IRP_MJ_QUERY_SECURITY 的 FLT_PARAMETERS</p>
<p>FltQuerySecurityObject</p>
<p>SeQuerySecurityDescriptorInfo</p>
<p>IRP_MJ_SET_SECURITY</p>
<p>IRP_MJ_SET_SECURITY 的 FLT_PARAMETERS</p>
<p>以下各项设置 SACL:</p>
<p>FltSetSecurityObject</p>
<p>SeSetSecurityDescriptorInfo</p>
<p>SeSetSecurityDescriptorInfoEx</p></td>
<td align="left"><p>需要在所有情况下 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PROCESS_TRUST_LABEL_SECURITY_INFORMATION</p></td>
<td align="left"><p>保留。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


Wdm.h 中 （包括 wdm.h 中）

## <a name="related-topics"></a>相关主题


[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)

[**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**SeQuerySecurityDescriptorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-sequerysecuritydescriptorinfo)

[**SeSetSecurityDescriptorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-sesetsecuritydescriptorinfo)

[**SeSetSecurityDescriptorInfoEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-sesetsecuritydescriptorinfoex)

[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)

[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)

 

 






