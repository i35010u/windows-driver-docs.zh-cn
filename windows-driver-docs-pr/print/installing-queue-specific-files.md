---
title: 安装队列特定的文件
description: 安装队列特定的文件
keywords:
- 指向和打印 WDK，特定队列的文件
- 队列特定文件 WDK 打印机
- 打印队列-WDK，点和打印
- 队列 WDK 打印机，指向和打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d007954f8bdbd724f0c34e166e4a19aaf277de0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835651"
---
# <a name="installing-queue-specific-files"></a>安装队列特定的文件





在安装打印机时，供应商提供的安装应用程序可以指定与特定打印队列关联的一组文件，这些文件属于任何类型。 文件将下载到连接到打印服务器的每个客户端。 安装应用程序通过在注册表中放置值来指定文件，如下表所示。

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
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Directory</strong></p></td>
<td><p>REG_SZ</p></td>
<td><p><strong>文件</strong>指定的文件的目录路径。 用作服务器上的源路径和客户端上的目标路径。 此路径相对于 PRINT $ 环境变量。</p></td>
</tr>
<tr class="even">
<td><p><strong>文件</strong></p></td>
<td><p>REG_MULTI_SZ</p></td>
<td><p>当客户端连接到打印服务器时要复制到客户端的文件的文件名。 文件可以是 Dll、数据文件或任何其他类型的文件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>模块</strong></p></td>
<td><p>REG_SZ</p></td>
<td><p>可选 <a href="point-and-print-dlls.md" data-raw-source="[Point and Print DLL](point-and-print-dlls.md)">点和打印 DLL</a>的文件名。</p></td>
</tr>
</tbody>
</table>

 

应用程序应通过调用打印后台处理程序的 **SetPrinterDataEx** 函数来创建这些值。 用此调用指定的注册表项的格式应为：

**CopyFiles \\**<em>ComponentName</em>

其中， *ComponentName* 是与文件相关联的软件组件的名称。 例如，在 **CopyFiles \\ icm** 项下指定与 Microsoft 图像颜色管理 (icm) 相关联的文件。 将注册表项名称指定为 **SetPrinterDataEx** 函数的参数，该函数将该键创建为打印服务器上打印队列的密钥的子项。

### <a name="installation-example"></a><a href="" id="ddk-installation-example-gg"></a>安装示例

例如，假设在打印服务器上安装了一个 HP Color LaserJet 打印机，并为其分配了打印队列名称 "HpColor"。 还假定 Microsoft ICM 需要以下两个文件与打印队列相关联：

-   名为 hpclrlsr 的颜色配置文件，位于服务器上的 "打印" 颜色中。 \\

-   名为 Mscms.dll 的 DLL，位于服务器上的 PRINT $ \\ 颜色中。

安装应用程序将调用 ICM API 函数 **AssociateColorProfileWithDevice**，该函数反过来调用 **SetPrinterDataEx** 来创建以下服务器注册表项：

```cpp
CopyFiles\ICM\Directory: Color
CopyFiles\ICM\Files: hpclrsr.icm
CopyFiles\ICM\Module: mscms.dll
```

Mscms.dll 模块是导出 **GenerateCopyFilePaths** 和 **SpoolerCopyFileEvent** 函数的 [点和打印 DLL](point-and-print-dlls.md) 。

 

 




