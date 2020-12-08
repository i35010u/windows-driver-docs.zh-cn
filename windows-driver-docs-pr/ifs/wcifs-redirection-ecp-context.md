---
title: WCIFS \_ 重定向 \_ ECP \_ 上下文结构
description: 描述特定创建操作的文件的重定向状态。
keywords:
- WCIFS_REDIRECTION_ECP_CONTEXT 结构可安装文件系统驱动程序
- PWCIFS_REDIRECTION_ECP_CONTEXT 结构指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- WCIFS_REDIRECTION_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ee87f1b2bbe69d46cad76377d42a8c14479f873
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813193"
---
# <a name="wcifs_redirection_ecp_context-structure"></a>WCIFS \_ 重定向 \_ ECP \_ 上下文结构


描述特定创建操作的文件的重定向状态。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _WCIFS_REDIRECTION_ECP_CONTEXT {
  USHORT      Size;
  USHORT      Flags;
  FILE_ID_128 FileId;
  GUID        VolumeGuid;
} WCIFS_REDIRECTION_ECP_CONTEXT, *PWCIFS_REDIRECTION_ECP_CONTEXT;
```

<a name="members"></a>成员
-------

**大小**  
结构的大小 `sizeof(WCIFS_REDIRECTION_ECP_CONTEXT)` 。

**标记**  
指示文件的重定向状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER</strong> 0x0001</td>
<td align="left"><p>这是未在 LayerRootLocations 注册表项中注册的层的重定向文件。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-scratch"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_SCRATCH</strong> 0x0002</td>
<td align="left"><p>这是一个新的或已修改的文件，不会重定向。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-registered-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REGISTERED_LAYER</strong> 0x0004</td>
<td align="left"><p>这是 LayerRootLocations 注册表项中列出的层的重定向文件。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-remote-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REMOTE_LAYER</strong> 0x0008</td>
<td align="left"><p>这是相对于容器的远程文件系统的重定向文件。 它不一定会在该服务器上注册为一个层。 对于 Hyper-v 容器，远程服务器是 Hyper-v 容器实用程序 VM 的主机。</p></td>
</tr>
</tbody>
</table>

 

**FileId**  
后备文件的标识符。

**VolumeGuid**  
备份文件所在的磁盘卷的基于 GUID 的标识符。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10 版本 1607</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

 

 





