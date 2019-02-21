---
title: 网络 INF 文件中的版本部分
description: 网络 INF 文件中的版本部分
ms.assetid: c76151e9-fef2-4bfe-8587-d58d95d234bc
keywords:
- INF 文件 WDK 网络，版本部分
- 可使用网络 INF 文件 WDK，版本部分
- 版本部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f46f9c7a5a95b1d2163f2ea4857b84b1aa40ba4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522475"
---
# <a name="version-section-in-a-network-inf-file"></a>网络 INF 文件中的版本部分





**版本**网络 INF 文件中的部分基于泛型[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)。

**版本**网络 INF 文件中的节具有以下特定于网络的条目：

-   [类](#class)
-   [ClassGuid](#classguid)
-   [签名和操作系统条目](#signature-and-operating-system-entries)
-   [PnpLockDown](#pnplockdown)
-   [CatalogFile](#catalogfile)
-   [版本的部分示例](#version-section-example)

### <a name="class"></a>类

**版本**部分应包含**类**条目标识文件安装的网络组件的类。

有四个网络类：

<a href="" id="net"></a>**Net**  
指定物理或虚拟网络适配器。 NDIS 中间驱动程序，它将导出的虚拟网络适配器，包含在 Net 类中。

<a href="" id="nettrans"></a>**NetTrans**  
指定网络协议，如 TCP/IP、 IPX、 面向连接的客户端或面向连接的呼叫管理器。

<a href="" id="netclient"></a>**NetClient**  
指定的网络客户端，如 Microsoft 客户端的网络或 NetWare 客户端。 NetClient 组件被视为网络提供商，并且如果通过网络提供打印服务，它也被视为是打印提供程序。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

<a href="" id="netservice"></a>**NetService**  
指定网络服务，如文件服务或打印服务。

**请注意**  红外数据协会 (IrDA) 合规的设备未归类为任何以前的四个网络类，即使它们由网络类安装程序安装。 用于安装 IrDA 设备 INF 文件应具有**类**的值**红外**。 此类包括序列红外线 （ir） 和快速红外线 （ir） 设备。

 

**请注意**  IrDA 微型端口驱动程序的支持已从 NDIS 6.30 (Windows 8) 及更高版本。

 

### <a name="classguid"></a>ClassGuid

**版本**部分必须包含**ClassGuid**条目。 网络类安装程序使用**ClassGuid**条目，以确定正在安装的网络组件的类。

有四个网络**ClassGuid**值，其中每个对应于网络类：

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
<td align="left"><p><strong>NetService</strong></p></td>
<td align="left"><p>{4D36E974-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
</tbody>
</table>

 

IrDA 设备 INF 文件应具有**ClassGuid**的值

{6bdd1fc5-81d0-bec7-08002be2092f}.

### <a name="signature-and-operating-system-entries"></a>签名和操作系统条目

**签名**条目必须 **$Windows NT$**。

### <a name="pnplockdown"></a>PnpLockDown

**PnpLockDown**条目应设置为 1，以防止应用程序直接修改驱动程序包的 INF 文件指定的文件。 有关此项的详细信息，请参阅[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)。

### <a name="catalogfile"></a>CatalogFile

**CatalogFile**条目用于声明的可选驱动程序所提供的.cat 文件。 有关详细信息，请参阅的供应商提供的文件部分[组件和文件用于网络组件安装](components-and-files-used-for-network-component-installation.md)。

### <a name="version-section-example"></a>版本的部分示例

以下是一种**版本**部分，了解安装的网络适配器的 INF 文件：

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

**请注意**   **提供程序**项均表示 INF 文件，不按的 INF 文件安装的组件的开发人员的开发人员。

 

 

 





