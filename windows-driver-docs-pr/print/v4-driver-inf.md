---
title: V4 驱动程序 INF
description: V4 打印驱动程序安装程序模型仍会继续使用 INF 文件，但还使用了新的清单文件以捕获打印机特定的安装程序指令。
ms.assetid: 48F19796-43F9-4A69-B042-1305245C9CB9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c641762929e4619a4c15762878bd730d2e8e2f3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358703"
---
# <a name="v4-driver-inf"></a>V4 驱动程序 INF


V4 打印驱动程序安装程序模型仍会继续使用 INF 文件，但还使用了新的清单文件以捕获打印机特定的安装程序指令。

## <a name="sample-inf"></a>示例 INF


请注意，示例的 v4 打印驱动程序 INF 文件，本主题中不包含任何特定于打印机的指令。 特定于打印机的说明包含在 v4 清单文件，其名称始终为结尾"– manifest.ini"。 驱动程序包中的每个驱动程序，可以指定其自己 v4 的清单文件。

下面的示例 INF 文件假定一个虚构的公司，Fabrikam，具有制造打印设备，它将安装为运行通过 v4 打印驱动程序。

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


下表显示在 v4 打印驱动程序和打印类驱动程序中允许的特定于打印机的指令的列表。

| 指令 | 描述                                         | 限制                                                                                                                                           | 用法        |
|-----------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| ClassVer  | 用于指示打印机类驱动程序是 v4。 | V4 打印驱动程序必须指定 ClassVer = 4.0。 V3 打印驱动程序可以指定 ClassVer = 3.0，但它是可选的。 这一次不支持任何其他值。 | ClassVer=4.0 |

## <a name="the-destinationdirs-keyword"></a>DestinationDirs 关键字


V4 驱动程序 INF 需要**DestinationDir**指定包中的所有文件。 受支持**DestinationDir**下表列出了值。

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
<td><p>[此目标 ID 为 v4 驱动程序已重载]</p>
<p>V4:这必须设置为 DefaultDestDir v4 打印驱动程序。 指定应从驱动程序存储区运行这些文件。</p>
<p>V3:这将指定文件应安装到 \3 目录。</p></td>
</tr>
<tr class="even">
<td>23</td>
<td><p>V4:此属性必须设置为<strong>DestinationDir</strong>任何颜色配置文件。</p>
<p>V3:应使用特定于打印机的 DirID 66003 安装颜色配置文件。</p></td>
</tr>
</tbody>
</table>

 

## <a name="inf-restrictions"></a>INF 限制


V4 打印驱动程序无需定义其他特定于打印机的指令或调出下面的列表中的关键字。

| INF 文件关键字            | 使用类型         |
|-----------------------------|--------------------|
| AddInterface                | 指令          |
| AddReg                      | 指令          |
| AddService                  | 指令          |
| BitReg                      | 指令          |
| ClassInstall32              | 部分类型       |
| ClassInstall32.Service      | 部分类型       |
| ConfigFile                  | v3 打印指令 |
| CoreDriverDependencies      | v3 打印指令 |
| CoreDriverSections          | v3 打印指令 |
| DataFile                    | v3 打印指令 |
| DDInstall.CoInstallers      | 部分类型       |
| DDInstall.FactDef           | 部分类型       |
| DDInstall.HW                | 部分类型       |
| DDInstall.Interfaces        | 部分类型       |
| DDInstall.LogConfigOverride | 部分类型       |
| DDInstall.Services          | 部分类型       |
| DDInstall.WMI               | 部分类型       |
| DefaultInstall              | 部分类型       |
| DefaultInstall.Services     | 部分类型       |
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
| InterfaceInstall32          | 部分类型       |
| LayoutFile                  | 指令          |
| LogConfig                   | 指令          |
| 需求                       | 指令          |
| PackageAware                | v3 打印指令 |
| RenFiles                    | 指令          |
| UpdateIniFields             | 指令          |
| UpdateInis                  | 指令          |

 

**NTPrint 引用**。 在清单文件中进行 NTPrint 引用。 INF 文件不需要有关其 DDInstall、 CopyFiles 或 SourceDisksFiles 部分中的 NTPrint 引用的任何信息。

**配置模块引用**。 所有打印驱动程序使用相同配置模块二进制文件 (PrintConfig.dll);没有选择配置模块的驱动程序的机制。

有关如何创建基本 v4 打印机驱动程序的 INF 文件的信息，请参阅[构建基本 v4 打印机驱动程序](building-a-basic-v4-printer-driver.md)。

 

 




