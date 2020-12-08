---
title: 打印驱动程序版本控制
description: 打印驱动程序版本控制
keywords:
- 安装驱动程序 WDK 打印机，版本控制
- 打印机驱动程序安装 WDK，版本控制
- 版本号 WDK 打印机
- 打印机驱动程序版本控制 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4e7cb9f11d555a557bb4bafd4b37ad6c37bfe9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807479"
---
# <a name="print-driver-versioning"></a>打印驱动程序版本控制





基于 Unidrv 和 Pscript5 的打印机微型驱动程序，以及由 IHV) 完全开发 (驱动程序的单一打印机驱动程序，应在 Microsoft Windows XP 和更高版本上使用打印机驱动程序版本控制。 Windows XP 和更高版本的打印后台处理程序使用版本控制信息，使其在安装新的操作系统版本或 Service Pack 的过程中或在建立新的点和打印连接时选择正确的驱动程序文件。

Windows 2000 或以前的基于 NT 的操作系统版本不支持打印机驱动程序版本控制。 在这些操作系统版本中，打印后台处理程序将决定是否仅根据文件时间戳替换特定驱动程序文件。 对于较旧的文件，始终选择较新的文件，即使具有较新日期的文件可能具有旧功能集。 由于可以轻松地更改文件的日期，因此这会阻止后台处理程序在其选择的文件中做出正确的选择。

若要确保安装正确版本的驱动程序文件，只需将版本号添加到这些文件中。 为此，可以对 Windows 驱动程序) 工具包 (附带的 pdrvver \[ \] ，并将该文件包含在打印机驱动程序 DLL 资源文件中。 设置单一驱动程序，使用基于 INF 的安装也可以从驱动程序版本控制中受益，因为较旧的 dll 不会覆盖较新的 dll，即使较旧的 DLL 可能有较新的时间戳。

Pdrvver 标头几乎只包含预处理器 \# 定义指令。 前两个版本的 \_ 文件类型和版本 \_ FILESUBTYPE （不得修改）指示该文件是驱动程序的资源文件，尤其是打印机驱动程序。 在 \_ \_ \_ VS FILESUBTYPE 结构的 Microsoft Windows SDK 文档中介绍了 VFT Winspool.drv 和 VFT2 Winspool.drv 版本控制 \_ 打印机，其中包含版本 \_ 类型和版本 \_ FIXEDFILEINFO \_ 。 ) 需要更改的常量是最后四项，如下所示： (

<a href="" id="ver-fileversion"></a>VER \_ FILEVERSION  
应将此常量设置为由四个逗号分隔的单词值组成的序列。 第三个和第四个单词用于分别设置 VS \_ FIXEDFILEINFO 结构的 **dwFileVersionLS** 成员的高位字和下限字。 下表中描述了每个单词的含义：

“值”

含义

第一个字

保留。 应将此值设置为0。

第二个词

表示驱动程序的主版本。 对于用户模式驱动程序，将此项设置为0x0003。 对于内核模式驱动程序，将此项设置为0x0002。

第三个词

表示功能集编号。

高字节

表示主要功能集版本。 建议使用较新的版本，使其成为以前版本的功能的超集。 将此值与每个新的主要版本递增。

对于在 Windows XP 及更高版本（包括 Windows 更新和 Service Pack）上运行的基于 Unidrv 和 Pscript5 的微型驱动程序，此设置应设置为0x05。

低字节

表示次要功能集版本-来自相同基本代码或体系结构的新版本。 将此值与每个新的次要版本递增。

对于在以下操作系统版本上运行的基于 Unidrv 和 Pscript5 的微型驱动程序，应按如下所示设置此字节：

Windows XP：设置为0x01。

第一个 Windows XP Service Pack：设置为0x01。  (第四个单词中出现特定的 bug 修复号。 ) 

第一个 Windows 更新：设置为0x02。

第四个词

表示 bug 修复或 Service Pack 版本。 当新的二进制文件是 bug 修复或 Service Pack 的集合时，增加此值。

 

下面是一个整体驱动程序示例：

```cpp
#define VER_FILEVERSION    0, 3, 0X0100, 0X0002
```

按照从左到右的顺序，第一个单词值为零，该值必须为零。 第二个单词的值为3，表示这是用户模式驱动程序。 在第三个字中，高字节的值 (0X01) 表示这是第一个主版本，同一个单词的低字节 (0x00) 指示目前有，没有次要版本。 第四个单词 (0x0002) 指示这是第二个 bug 修复或 Service Pack 发布。  (不区分这两种类型的版本。 ) 

下面是一些 Unidrv/Pscript5-based 微型驱动程序示例：

```cpp
#define VER_FILEVERSION    0, 3, 0X0501, 0X0001
```

按照从左到右的顺序，第一个单词值为零，与之前相同。 第二个单词的值为3，表示这是用户模式驱动程序。 在第三个字中，高字节和低字节值分别 (0X05 和 0x01) 表示此版本适用于 Windows XP。 第四个单词 (0x0001) 指示这是第一个 bug 修复或 Service Pack 发布。

```cpp
#define VER_FILEVERSION    0, 3, 0X0502, 0X0000
```

与前面一样，第一个单词为零，第二个单词指示这是用户模式的微型驱动程序。 第三个单词 (0x0502) 指示这是 Windows XP 之后发布的第一个 Windows 更新版本。 第四个单词 (0x0000) 指示这既不是 bug 修复也不 Service Pack 发布。

<a href="" id="ver-filedescription-str"></a>VER \_ FILEDESCRIPTION \_ STR  
应将此常量设置为标识该驱动程序的名称，如以下示例中所示。

```cpp
#define VER_FILEDESCRIPTION_STR    "Sample Printer Driver Resource DLL"
```

<a href="" id="ver-internalname-str"></a>VER \_ INTERNALNAME \_ STR  
将此常量设置为指定文件内部名称的名称， (不包括路径) ，如以下示例中所示。 有关详细信息，请参阅 Windows SDK 文档。

```cpp
#define VER_INTERNALNAME_STR    "SAMPLERES.DLL"
```

<a href="" id="ver-originalfilename-str"></a>VER \_ ORIGINALFILENAME \_ STR  
将此常量设置为一个名称，该名称指定文件的原始名称 (不包括路径) ，如以下示例中所示。 有关详细信息，请参阅 Windows SDK 文档。

```cpp
#define VER_ORIGINALFILENAME_STR    "SAMPLERES.DLL"
```

 

 




