---
title: 打印驱动程序版本控制
description: 打印驱动程序版本控制
ms.assetid: 8ce844a5-44f6-4967-8586-b302823fc862
keywords:
- 安装驱动程序 WDK 打印机、 版本控制
- 打印机驱动程序安装 WDK、 版本控制
- 版本编号 WDK 打印机
- 打印机驱动程序版本控制 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2766f0f4de62a036b03612b71df86780e3fdb4e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358238"
---
# <a name="print-driver-versioning"></a>打印驱动程序版本控制





基于 Unidrv 和 Pscript5 的打印机微型驱动程序，以及整体化打印机驱动程序 （驱动程序完全由 IHV 开发），应使用 Microsoft Windows XP 及更高版本的打印机驱动程序版本控制。 Windows XP 和更高版本的打印后台处理程序使用的版本控制信息以使其能够在安装新操作系统版本或 service pack，或建立新的指向和打印连接过程中选择正确的驱动程序文件。

打印机驱动程序版本控制不支持在 Windows 2000 或早期基于 NT 的操作系统版本上。 在这些操作系统版本中，打印后台处理程序基于其决定是否要替换的特定驱动程序文件仅在文件的时间戳。 即使具有较新日期的文件可能具有的旧功能集，将始终优先较旧的文件，选择较新的文件。 因为它是可以十分轻松地更改文件的日期，这样可以防止后台处理程序在它选择的文件中做出正确的选择。

若要确保安装了正确版本的驱动程序文件，只需对这些文件添加版本号。 您可以执行此操作，从而为 pdrvver.h 稍作修改 (Windows 驱动程序工具包附带的\[WDK\])，并在打印机驱动程序 DLL 的资源文件中包括该文件。 整体化驱动程序进行设置，使用基于 INF 的安装，还受益于驱动程序版本控制，因为更高版本的 DLL 不会覆盖较旧的 DLL，即使较旧的 DLL 可能具有较新的时间戳。

Pdrvver.h 标头以独占方式几乎包含预处理器\#定义指令。 前两个，VER\_FILETYPE 和 VER\_FILESUBTYPE，不得修改指示文件是驱动程序，专门的打印机驱动程序的资源文件。 (常量 VFT\_DRV 和 VFT2\_DRV\_VERSIONED\_打印机出现 VER\_FILETYPE 和 VER\_FILESUBTYPE，Microsoft Windows SDK 中介绍文档 VS\_FIXEDFILEINFO 结构。)您需要更改的是最后四个，如下所示：

<a href="" id="ver-fileversion"></a>VER\_的文件版本  
此常量应设置为一系列以逗号分隔的四个 WORD 值。 第三个和第四个单词用于设置高和低的单词，分别在 vs\_FIXEDFILEINFO 结构**dwFileVersionLS**成员。 下表中描述了每个四个词的含义：

ReplTest1

含义

第一个单词

保留。 此值应设置为 0。

第二个字

表示该驱动程序的主版本。 对于用户模式驱动程序，将其设置到 0x0003。 对于内核模式驱动程序，将其设置到 0x0002。

第三个单词

表示功能组数。

高字节

表示为主要功能集发布。 较新版本则假设的以前的版本中的功能超集。 增加此值与每个新的主版本。

对于基于 Unidrv 和 Pscript5 的微型驱动程序运行 Windows XP 及更高版本，包括 Windows 更新和 Service Pack，这应设置到 0x05:sp。

低字节

表示细微的功能集发行版-从同一基本代码或体系结构的新版本。 增加此值与每个新次要版本。

对于基于 Unidrv 和 Pscript5 的微型驱动程序在以下操作系统版本上运行，应设置此字节所示：

Windows XP:设置为 0x01。

第一个 Windows XP Service Pack:设置为 0x01。 （特定的 bug 修复，数在第四个 WORD 中显示。）

第一个 Windows 更新：设置为 0x02。

第四个单词

表示的 bug 修补程序或服务包版本。 它是集合的 bug 修补程序或服务包时递增上发布新的二进制文件，此值。

 

下面是一个整体化驱动程序示例：

```cpp
#define VER_FILEVERSION    0, 3, 0X0100, 0X0002
```

按顺序从左到右，第一个字值为零，它必须是。 第二个字的值为 3，表明这用户模式驱动程序。 在第三个 WORD 中，高字节值 (0X01) 表示这是第一个主要版本，并且相同的单词 (0x00) 的低位字节表示，到目前为止，没有次要版本。 第四个单词 (0x0002) 指示这是第二个 bug 修补程序或服务包版本。 （不区分这些类型的版本。）

以下是一些 Unidrv-/ 基于 Pscript5 的微型驱动程序示例：

```cpp
#define VER_FILEVERSION    0, 3, 0X0501, 0X0001
```

按顺序从左到右，第一个字值为零，像以前一样。 第二个字的值为 3，表明这用户模式驱动程序。 在第三个单词、 高字节和低字节值 (0x05:sp 和 0x01，分别) 表示这是适用于 Windows XP 版本。 第四个单词 (0x0001) 指示这是第一个 bug 修补程序或服务包版本。

```cpp
#define VER_FILEVERSION    0, 3, 0X0502, 0X0000
```

如之前，第一个字为零，且第二个 WORD 指示这是用户模式下微型驱动程序。 第三个单词 (0x0502) 指示这是在 Windows XP 之后发布的第一个 Windows 更新版本。 第四个单词 (0x0000) 指示这是既没有的 bug 修复，也没有服务包版本。

<a href="" id="ver-filedescription-str"></a>VER\_FILEDESCRIPTION\_STR  
此常量应设置为用于标识该驱动程序，如以下示例所示的名称。

```cpp
#define VER_FILEDESCRIPTION_STR    "Sample Printer Driver Resource DLL"
```

<a href="" id="ver-internalname-str"></a>VER\_INTERNALNAME\_STR  
将此常量设置为指定的文件 （不包括路径） 的内部名称，如以下示例所示的名称。 有关详细信息，请参阅 Windows SDK 文档。

```cpp
#define VER_INTERNALNAME_STR    "SAMPLERES.DLL"
```

<a href="" id="ver-originalfilename-str"></a>VER\_ORIGINALFILENAME\_STR  
将此常量设置为指定的文件 （不包括路径） 的原始名称，如以下示例所示的名称。 有关详细信息，请参阅 Windows SDK 文档。

```cpp
#define VER_ORIGINALFILENAME_STR    "SAMPLERES.DLL"
```

 

 




