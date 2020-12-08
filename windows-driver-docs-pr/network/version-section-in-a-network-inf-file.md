---
title: 网络 INF 文件中的 Version 节
description: 网络 INF 文件中的 Version 节
keywords:
- INF 文件 WDK 网络，版本部分
- 网络 INF 文件 WDK，版本部分
- 版本部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f1764d332c69cb09cb4f72a5bfa8a2a6c23d01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839219"
---
# <a name="version-section-in-a-network-inf-file"></a>网络 INF 文件中的 Version 节





网络 INF 文件中的 **版本** 部分基于通用 [**INF 版本部分**](../install/inf-version-section.md)。

网络 INF 文件中的 **版本** 部分具有以下特定于网络的条目：

-   [类](#class)
-   [ClassGuid](#classguid)
-   [签名和操作系统条目](#signature-and-operating-system-entries)
-   [PnpLockDown](#pnplockdown)
-   [CatalogFile](#catalogfile)
-   [版本部分示例](#version-section-example)

### <a name="class"></a>类

**版本** 部分应包含一个 **类** 条目，该条目标识文件安装的网络组件的类。

有四个网络类：

<a href="" id="net"></a>**Net**  
指定物理或虚拟网络适配器。 导出虚拟网络适配器的 NDIS 中间驱动程序包含在 .Net 类中。

<a href="" id="nettrans"></a>**NetTrans**  
指定网络协议，如 TCP/IP、IPX、面向连接的客户端或面向连接的呼叫管理器。

<a href="" id="netclient"></a>**NetClient**  
指定网络客户端，如用于网络的 Microsoft 客户端或 NetWare 客户端。 NetClient 组件被视为网络提供程序，如果它通过网络提供打印服务，它也被视为打印提供程序。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

<a href="" id="netservice"></a>**空间**  
指定网络服务，例如文件服务或打印服务。

**注意**  红外数据关联 (IrDA) 兼容设备未分类为之前四个网络类中的任何一个，即使它们是由网络类安装程序安装的。 用于安装 IrDA 设备的 INF 文件的 **类** 值应为 " **红外**"。 此类包括串行 IR 和快速 IR 设备。

 

**注意**  已从 NDIS 6.30 (Windows 8) 和更高版本中删除了对 IrDA 微型端口驱动程序的支持。

 

### <a name="classguid"></a>ClassGuid

**版本** 部分必须包含 **ClassGuid** 条目。 网络类安装程序使用 **ClassGuid** 项来确定要安装的网络组件的类。

有四个网络 **ClassGuid** 值，其中每个值对应于一个网络类：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">网络类</th>
<th align="left">ClassGuid</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Net</strong></p></td>
<td align="left"><p>{4D36E972-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NetTrans</strong></p></td>
<td align="left"><p>{4D36E975-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NetClient</strong></p></td>
<td align="left"><p>{4D36E973-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>空间</strong></p></td>
<td align="left"><p>{4D36E974-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
</tbody>
</table>

 

IrDA 设备的 INF 文件的 **ClassGuid** 值应为

{6bdd1fc5-81d0-bec7-08002be2092f}.

### <a name="signature-and-operating-system-entries"></a>签名和操作系统条目

**签名** 条目必须 **$Windows NT $**。

### <a name="pnplockdown"></a>PnpLockDown

**PnpLockDown** 项应设置为1，以防止应用程序直接修改驱动程序包的 INF 文件指定的文件。 有关此项的详细信息，请参阅 [**INF 版本部分**](../install/inf-version-section.md)。

### <a name="catalogfile"></a>CatalogFile

**CatalogFile** 项用于声明可选的驱动程序提供的 .cat 文件。 有关详细信息，请参阅 [用于网络组件安装的组件和文件](components-and-files-used-for-network-component-installation.md)的供应商提供的文件部分。

### <a name="version-section-example"></a>版本部分示例

下面是用于安装网络适配器的 INF 文件的 **版本** 部分示例：

```INF
[Version]
Signature = $Windows NT$
Class=Net
ClassGuid = {4D36E972-E325-11CE-BFC1-08002BE10318}
Provider = %Msft%
DriverVer=06/22/2010,6.1.7065.0
PnpLockDown = 1
CatalogFile = netvmini630.cat
```

**注意**  
**提供程序** 项指示 inf 文件的开发人员，而不是 inf 文件所安装组件的开发人员。

 

 

