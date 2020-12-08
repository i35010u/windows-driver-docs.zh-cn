---
title: V4 驱动程序 INF
description: V4 打印驱动程序安装模型继续使用 INF 文件，但也使用新的清单文件来捕获打印机特定的安装指令。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 381a1266581a22839829c19de022c50becf2a0b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785937"
---
# <a name="v4-driver-inf"></a>V4 驱动程序 INF


V4 打印驱动程序安装模型继续使用 INF 文件，但也使用新的清单文件来捕获打印机特定的安装指令。

## <a name="sample-inf"></a>示例 INF


请注意，本主题中介绍的示例 v4 打印驱动程序 INF 文件不包含任何特定于打印机的指令。 特定于打印机的指令包含在 v4 清单文件中，该文件始终以 "– manifest.ini" 结尾。 驱动程序包中的每个驱动程序都可以指定其自己的 v4 清单文件。

以下示例 INF 文件假设虚构公司 Fabrikam 具有制造打印设备，这些设备将安装为与 v4 打印驱动程序一起运行。

```INF
[Version]
Signature="$Windows NT$"
Provider="Fabrikam"
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer
CatalogFile=prnfa999.CAT
DriverVer=09/12/2010,6.2.8060.4
ClassVer=4.0 ;This causes v4 setup to take place

[Manufacturer]
"Fabrikam"=Fabrikam,NTamd64

[Fabrikam.NTamd64] ;Add your models here
"Fabrikam Laser 9000" =        Laser9000,Fabrik9000_sdfjkals                     ;HWID example
"Fabrikam Laser 9100" =        Laser9000,Fabrik9100_sjkasj                       ;HWID example
"Fabrikam Laser 9000 series" = Laser9000,{E0691E8C-F7CC-456E-A7B5-D1FC19BA2279}  ;PrinterDriverID

[Laser9000]
CopyFiles=Laser9000_FILES

[Laser9000_FILES]
faPDL.gpd
faPDL-pipelineconfig.xml
faPDL-manifest.ini
faPDL.dll

[SourceDisksNames.amd64]
1 = %Location%,,,
2 = %Location%,,,amd64

[SourceDisksNames.x86]
1 = %Location%,,,
2 = %Location%,,,x86

[DestinationDirs]
DefaultDestDir=66000

[SourceDisksFiles]
faPDL.gpd=1
faPDL-pipelineconfig.xml=1
faPDL-manifest.ini = 1
faPDL.dll =2

[Strings]
Location="Fabrikam DVD"
```

## <a name="inf-directives"></a>INF 指令


下表显示了在 v4 打印驱动程序和打印类驱动程序中允许使用的特定于打印机的指令的列表。

| 指令 | 描述                                         | 限制                                                                                                                                           | 使用情况        |
|-----------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| ClassVer  | 用于指示打印机类驱动程序为 v4。 | V4 打印驱动程序必须指定 ClassVer = 4.0。 V3 打印驱动程序可以指定 ClassVer = 3.0，但这是可选的。 此时不支持其他值。 | ClassVer = 4。0 |

## <a name="the-destinationdirs-keyword"></a>DestinationDirs 关键字


V4 驱动程序 INF 要求为包中的所有文件指定 **DestinationDir** 。 下表列出了支持的 **DestinationDir** 值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DestinationDir ID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>66000</td>
<td><p>[V4 驱动程序的此目标 ID 已过载]</p>
<p>V4：必须将其设置为 v4 打印驱动程序的 DefaultDestDir。 指定应从驱动程序存储区中运行文件。</p>
<p>V3：指定应将文件安装到 "-3" 目录。</p></td>
</tr>
<tr class="even">
<td>23</td>
<td><p>V4：必须将其设置为任何颜色配置文件的 <strong>DestinationDir</strong> 。</p>
<p>V3：应使用打印机特定的 DirID 66003 安装颜色配置文件。</p></td>
</tr>
</tbody>
</table>

 

## <a name="inf-restrictions"></a>INF 限制


V4 打印驱动程序不能在以下列表中定义其他特定于打印机的指令或关键字。

| INF 文件关键字            | 使用类型         |
|-----------------------------|--------------------|
| AddInterface                | 指令          |
| AddReg                      | 指令          |
| AddService                  | 指令          |
| BitReg                      | 指令          |
| ClassInstall32              | 节类型       |
| ClassInstall32。服务      | 节类型       |
| ConfigFile                  | v3 打印指令 |
| CoreDriverDependencies      | v3 打印指令 |
| CoreDriverSections          | v3 打印指令 |
| DataFile                    | v3 打印指令 |
| DDInstall.CoInstallers      | 节类型       |
| DDInstall.FactDef           | 节类型       |
| DDInstall                | 节类型       |
| DDInstall 接口        | 节类型       |
| DDInstall.LogConfigOverride | 节类型       |
| DDInstall          | 节类型       |
| DDInstall               | 节类型       |
| DefaultInstall              | 节类型       |
| DefaultInstall     | 节类型       |
| DelFiles                    | 指令          |
| DelReg                      | 指令          |
| DelService                  | 指令          |
| DontReflectOffline          | 指令          |
| DriverFile                  | v3 打印指令 |
| DriverIsolation             | v3 打印指令 |
| FeatureScore                | 指令          |
| HelpFile                    | v3 打印指令 |
| 包括                     | 指令          |
| Ini2Reg                     | 指令          |
| InterfaceInstall32          | 节类型       |
| LayoutFile                  | 指令          |
| LogConfig                   | 指令          |
| 需求                       | 指令          |
| PackageAware                | v3 打印指令 |
| RenFiles                    | 指令          |
| UpdateIniFields             | 指令          |
| UpdateInis                  | 指令          |

 

**Ntprint.inf 引用**。 Ntprint.inf 在清单文件中进行引用。 INF 文件不需要有关其 DDInstall、CopyFiles 或 SourceDisksFiles 部分中的 Ntprint.inf 引用的任何信息。

**配置模块引用**。 所有打印驱动程序使用相同的配置模块二进制 ( # A0) ;驱动程序没有选择配置模块的机制。

有关如何创建基本 v4 打印机驱动程序的 INF 文件的信息，请参阅 [构建基本 V4 打印机驱动程序](building-a-basic-v4-printer-driver.md)。

 

 




