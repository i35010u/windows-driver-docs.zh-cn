---
title: WCIFS\_重定向\_ECP\_上下文结构
description: 本文介绍特定于创建操作的文件重定向状态。
ms.assetid: 6101490D-54B9-4A34-ADB5-9CC2B855691D
keywords:
- WCIFS_REDIRECTION_ECP_CONTEXT 结构可安装文件系统驱动程序
- PWCIFS_REDIRECTION_ECP_CONTEXT 结构指针可安装文件系统驱动程序
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
ms.openlocfilehash: d0c61818f522849d9738d622feee193944ff2faa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521525"
---
# <a name="wcifsredirectionecpcontext-structure"></a>WCIFS\_重定向\_ECP\_上下文结构


本文介绍特定于创建操作的文件重定向状态。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _WCIFS_REDIRECTION_ECP_CONTEXT {
  USHORT      Size;
  USHORT      Flags;
  FILE_ID_128 FileId;
  GUID        VolumeGuid;
} WCIFS_REDIRECTION_ECP_CONTEXT, *PWCIFS_REDIRECTION_ECP_CONTEXT;
```

<a name="members"></a>成员
-------

**大小**  
结构的大小`sizeof(WCIFS_REDIRECTION_ECP_CONTEXT)`。

**标志**  
指示文件的重定向状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER</strong> 0x0001</td>
<td align="left"><p>这是从一个层，用于在 LayerRootLocations 注册表项中未注册重定向的文件。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-scratch"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_SCRATCH</strong> 0x0002</td>
<td align="left"><p>这是一个新的或修改文件，它不会重定向。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-registered-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REGISTERED_LAYER</strong> 0x0004</td>
<td align="left"><p>这是从一个层 LayerRootLocations 注册表项中列出的重定向的文件。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="" id="wcifs-redirection-flags-create-serviced-from-remote-layer"></a>
<strong>WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REMOTE_LAYER</strong> 0x0008</td>
<td align="left"><p>这是从远程文件系统容器相对的重定向的文件。 它可能会或可能未注册为该服务器上的层。 HYPER-V 容器的远程服务器是 HYPER-V 容器实用程序 VM 的主机。</p></td>
</tr>
</tbody>
</table>

 

**FileId**  
备份文件的标识符。

**VolumeGuid**  
备份文件所在的位置的磁盘卷的基于 GUID 的标识符。

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
<td align="left"><p>Windows 10，版本 1607</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

 

 





