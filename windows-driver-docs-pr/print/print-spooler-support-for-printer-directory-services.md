---
title: 打印机目录服务的打印后台处理程序支持
description: 打印机目录服务的打印后台处理程序支持
ms.assetid: 23cd73a5-8628-4471-a6c6-e056536fcc75
keywords:
- 目录服务 WDK 打印机
- 打印后台处理程序目录服务支持 WDK
- 发布 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170dc2f1756fbea5763d073cd001bed8bc3013e1
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242980"
---
# <a name="print-spooler-support-for-printer-directory-services"></a>打印机目录服务的打印后台处理程序支持





Windows 2000 和更高版本的目录服务的打印后台处理程序支持包括：

-   正在发布打印队列。

-   维护三个注册表项。

-   允许访问后台处理程序的注册表项。

-   返回打印队列的发布状态。

### <a href="" id="ddk-publishing-print-queues-gg"></a>发布打印队列

Microsoft Windows SDK 文档中所述的**SetPrinter**函数允许调用方发布、取消发布或更新打印队列对象。 为此，必须使用 PRINTER\_INFO\_7 的输入结构调用**SetPrinter**函数。

仅当打印队列对象与描述用户所连接到的打印服务器的计算机对象关联时，才能发布该对象。 用户发布打印队列的能力取决于用户的访问权限，该权限包含在用户的客户端安全上下文中。 如果对打印队列具有 "管理打印机" 权限，则可以发布打印队列。

### <a href="" id="ddk-maintaining-three-registry-keys-gg"></a>维护三个注册表项

三个注册表项包含在打印队列对象中发布的所有信息的副本。 使用 winspool.drv 中定义的以下标识符引用这三个键：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Key</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPLDS_DRIVER_KEY</p></td>
<td><p>用于存储驱动程序特定的信息，这些信息可由后台处理程序或驱动程序提供。</p></td>
</tr>
<tr class="even">
<td><p>SPLDS_SPOOLER_KEY</p></td>
<td><p>用于存储后台处理程序提供的特定于后台处理程序的信息。</p></td>
</tr>
<tr class="odd">
<td><p>SPLDS_USER_KEY</p></td>
<td><p>用于存储应用程序提供的用户特定的信息。</p></td>
</tr>
</tbody>
</table>

 

后台处理程序使用 SPLDS\_驱动程序\_密钥来存储可通过调用 Microsoft Windows SDK **DeviceCapabilities**函数获取的驱动程序功能。 驱动程序负责存储后台处理程序无法获取的驱动程序功能，如打印机[驱动程序对打印机目录服务的支持](printer-driver-support-for-printer-directory-services.md)中所述。 存储在这些注册表项下的值必须由 SPLDS 中定义的 **\_** 的常量标识，在 winspool.drv 中定义。

后台处理程序将跟踪自上次更新打印队列对象以来这些项下已修改了哪些值。 每次后台处理程序发布或更新打印队列对象时，都会将所有修改的值复制到对象中。

### <a href="" id="ddk-allowing-access-to-spooler-maintained-registry-keys-gg"></a>允许访问后台处理程序维护的注册表项

使用后台处理程序，打印机驱动程序可以通过调用**SetPrinterDataEx**、 **GetPrinterDataEx**和**EnumPrinterDataEx**函数来访问这三个后台处理程序维护的注册表项，Microsoft Windows SDK 文档中对这些功能进行了说明。 **SetPrinterDataEx**函数设置键下的值，而**GetPrinterDataEx**和**EnumPrinterDataEx**返回当前值。 （驱动程序不应在 SPLDS\_后台处理程序\_密钥键下设置值。）这些函数的调用方不指定完整的注册表路径;函数自动确定指定打印队列的注册表项的路径。

### <a href="" id="ddk-returning-a-print-queues-publication-state-gg"></a>返回打印队列的发布状态

Microsoft Windows SDK 文档中所述的**GetPrinter**函数允许调用方确定打印队列当前是否已发布。 为此，必须使用 PRINTER\_INFO\_7 的输入结构调用**GetPrinter**函数。 该函数返回打印队列的发布状态（已发布或未发布）和对象标识符。

Windows SDK 文档中介绍了前面提到的所有函数。 这些函数不是专门用于与 DS 相关的操作。

 

 




