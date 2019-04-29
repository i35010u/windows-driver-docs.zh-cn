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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372077"
---
# <a name="print-spooler-support-for-printer-directory-services"></a>打印机目录服务的打印后台处理程序支持





Windows 2000 和更高版本打印后台处理程序对目录服务包含的支持：

-   发布打印队列。

-   维护三个注册表项。

-   允许后台处理程序维护注册表项的访问。

-   返回的打印队列的发布状态。

### <a href="" id="ddk-publishing-print-queues-gg"></a>发布打印队列

**SetPrinter**函数，在 Microsoft Windows SDK 文档中，将会介绍允许调用方发布、 取消发布，或更新的打印队列对象。 出于这些目的**SetPrinter**函数的调用必须使用打印机的输入结构\_信息\_7。

仅当它是描述用户连接到打印服务器的计算机对象相关联，可以发布打印队列对象。 包含用户的客户端安全上下文中，通过其访问权限，确定发布打印队列的用户的能力。 如果打印队列上拥有管理打印机权限，可以将发布打印队列。

### <a href="" id="ddk-maintaining-three-registry-keys-gg"></a>维护三个注册表项

三个注册表项包含发布打印队列对象中的所有信息的副本。 使用 winspool.h 中定义的以下标识符引用三个密钥：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>键</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPLDS_DRIVER_KEY</p></td>
<td><p>用于存储特定于驱动程序的信息，可由后台处理程序或驱动程序提供。</p></td>
</tr>
<tr class="even">
<td><p>SPLDS_SPOOLER_KEY</p></td>
<td><p>用于存储后台处理程序提供特定于后台处理程序的信息。</p></td>
</tr>
<tr class="odd">
<td><p>SPLDS_USER_KEY</p></td>
<td><p>用于存储应用程序提供特定于用户的信息。</p></td>
</tr>
</tbody>
</table>

 

后台处理程序使用 SPLDS\_驱动程序\_键来存储驱动程序功能，可以通过调用 Microsoft Windows SDK 获取**DeviceCapabilities**函数。 该驱动程序是负责存储驱动程序功能，不能获取后台处理程序，如中所述[打印机目录服务的打印机驱动程序支持](printer-driver-support-for-printer-directory-services.md)。 这些项下存储的值必须由标识**SPLDS\_**-前缀 winspool.h 中定义的常量。

跟踪自上次更新的打印队列对象以来修改了这些项下的值的后台处理程序。 每次后台处理程序将发布或更新的打印队列对象，它复制到的对象所有已修改的值。

### <a href="" id="ddk-allowing-access-to-spooler-maintained-registry-keys-gg"></a>允许后台处理程序维护注册表项的访问

后台处理程序允许打印机驱动程序通过调用访问的三个后台处理程序维护注册表项**SetPrinterDataEx**， **GetPrinterDataEx**和**EnumPrinterDataEx**函数，所有这些 Microsoft Windows SDK 文档中所述。 **SetPrinterDataEx**函数设置项下的值时**GetPrinterDataEx**并**EnumPrinterDataEx**返回当前值。 (驱动程序不应设置值下 SPLDS\_后台处理程序\_密钥密钥。)这些函数的调用方未指定完整的注册表路径;函数会自动确定指定的打印队列的注册表项的路径。

### <a href="" id="ddk-returning-a-print-queues-publication-state-gg"></a>返回的打印队列的发布状态

**GetPrinter**函数，在 Microsoft Windows SDK 文档中，将会介绍允许调用方确定是否当前发布的打印队列。 为此，请**GetPrinter**函数的调用必须使用打印机的输入结构\_信息\_7。 该函数将返回打印队列的发布状态 （已发布或已取消发布） 和对象标识符。

Windows SDK 文档中介绍前面提到的所有函数。 函数不能以独占方式提供与 DS 相关的操作。

 

 




