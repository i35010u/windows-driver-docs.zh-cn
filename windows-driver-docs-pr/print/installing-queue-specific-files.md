---
title: 安装特定于队列的文件
description: 安装特定于队列的文件
ms.assetid: 86cb16d5-6035-4a4d-a6b7-f27ebd3e9f5c
keywords:
- 点和打印 WDK，特定于队列的文件
- 特定于队列的文件 WDK 打印机
- 打印队列 WDK 中，指向并打印
- 队列 WDK 打印机，指向并打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e022281cfbdc68ff209919f5de75c978f9a20bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524634"
---
# <a name="installing-queue-specific-files"></a>安装特定于队列的文件





在打印机安装时，供应商提供安装应用程序可以指定一组文件，任何类型，与特定的打印队列关联。 文件下载到每个客户端连接到打印服务器。 下表中所示，安装应用程序通过将值放在注册表中，指定的文件。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>值名称</th>
<th>值类型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Directory</strong></p></td>
<td><p>REG_SZ</p></td>
<td><p>为指定的文件的目录路径<strong>文件</strong>。 用作源路径在服务器上的和在客户端上的目标路径。 此路径是相对于打印 $ 环境变量。</p></td>
</tr>
<tr class="even">
<td><p><strong>文件</strong></p></td>
<td><p>REG_MULTI_SZ</p></td>
<td><p>文件的文件复制到客户端时客户端连接到打印服务器的名称。 文件可以是文件的 Dll、 数据文件或任何其他类型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>模块</strong></p></td>
<td><p>REG_SZ</p></td>
<td><p>可选文件名<a href="point-and-print-dlls.md" data-raw-source="[Point and Print DLL](point-and-print-dlls.md)">点和打印 DLL</a>。</p></td>
</tr>
</tbody>
</table>

 

应用程序应通过调用打印后台处理程序的创建这些值**SetPrinterDataEx**函数。 通过此调用指定的注册表项的格式应为：

**CopyFiles\\**<em>ComponentName</em>

其中*ComponentName*与文件相关联的软件组件的名称。 例如，在指定的文件关联与 Microsoft 图像颜色管理 (ICM) **CopyFiles\\ICM**密钥。 作为参数指定的注册表项名称**SetPrinterDataEx**函数，并且该函数创建的密钥作为打印服务器上的打印队列的项的子项。

### <a href="" id="ddk-installation-example-gg"></a>安装示例

例如，假设 HP 颜色激光打印机的打印服务器上安装并分配"HpColor"的打印队列名称。 此外，假定 Microsoft ICM 需要以下两个文件与打印队列相关联：

-   名为 hpclrlsr.icm，颜色配置文件位于 PRINT$\\在服务器上的颜色。

-   名为 Mscms.dll 的 DLL 位于 PRINT$\\在服务器上的颜色。

安装应用程序将调用 ICM API 函数**AssociateColorProfileWithDevice**，从而又会调用**SetPrinterDataEx** ，创建注册表项的以下服务器：

```cpp
CopyFiles\ICM\Directory: Color
CopyFiles\ICM\Files: hpclrsr.icm
CopyFiles\ICM\Module: mscms.dll
```

Mscms.dll 模块是[点和打印 DLL](point-and-print-dlls.md)导出**GenerateCopyFilePaths**并**SpoolerCopyFileEvent**函数。

 

 




