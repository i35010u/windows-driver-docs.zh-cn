---
title: 生成 BDA 驱动程序
description: 生成 BDA 驱动程序
ms.assetid: 2272fa18-5102-443e-8728-f256444ab044
keywords:
- 广播驱动程序体系结构 WDK AVStream，构建驱动程序
- BDA WDK AVStream，构建驱动程序
- 构建驱动程序 WDK，BDA
- 生成实用工具 WDK，BDA
- WDK BDA 宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0910e912280f1518422048e2afbd19d4682d8323
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575509"
---
# <a name="building-bda-drivers"></a>生成 BDA 驱动程序





**请注意**  开始 Windows 8，WDK 构建环境不再使用 Build.exe。 请参阅[WDK 和 Visual Studio 构建环境](https://msdn.microsoft.com/library/windows/hardware/hh454286)。 以下讨论仅适用于构建您的驱动程序使用 WDK Windows 7 版本或更早版本。

 

可以使用 Microsoft Windows Driver Kit (WDK) 来生成广播驱动程序体系结构 (BDA) 驱动程序。 若要生成 BDA 驱动程序，打开 WDK 构建环境窗口，更改为相应 BDA 驱动程序的源代码子目录的 WDK 的主要源目录，并使用**生成**命令。 **构建**命令将获取有关如何构建 BDA 驱动程序从说明*源*驻留在 BDA 驱动程序的源代码子目录中的文件。

有关生成实用工具、 WDK 的生成环境、 宏和环境变量用于控制生成实用工具和所需来生成 BDA 驱动程序文件的详细信息，请参阅"使用生成实用工具"和"生成实用程序参考"中Windows 7 WDK 文档 （内部版本 7600） 中。

以下列表包含宏名称用于 BDA*源*文件，并讨论了如何使用它们来生成 BDA 驱动程序：

<a href="" id="--------targetname-------"></a> TARGETNAME   
设置为 BDA 驱动程序的名称，以便当 WDK 生成该驱动程序时它用此名称生成。 下面的代码提供了一个示例：

```make
TARGETNAME=BDAsampl  # WDK builds the driver as BDAsampl.sys
```

<a href="" id="--------targetpath-------"></a> TARGETPATH   
为内置驱动程序设置的目标目录。 请注意，具体取决于你的生成环境是"免费"或"检查"，可以使用生成\_ALT\_DIR 变量以将"如 fre"或"chk"追加到\\obj 子目录的目录下创建生成命令包含*源*文件。 下面的代码提供了一个示例：

```make
TARGETPATH=obj$(BUILD_ALT_DIR) # built driver in \objfre or \objchk
```

<a href="" id="--------targettype-------"></a> TARGETTYPE   
设置要生成作为驱动程序 （而不是，例如，程序或 DLL），如下面的代码中所示的文件类型：

```make
TARGETTYPE=DRIVER  # WDK builds the driver as *.sys
```

<a href="" id="--------targetlibs-------"></a> TARGETLIBS   
指向 BDA 驱动程序的示例源必须链接到的库文件。 BDA 驱动程序至少必须链接到库，下面的代码示例中所示：

```make
TARGETLIBS=..\..\..\..\lib\ks.lib \
           ..\..\..\..\lib\ksguid.lib \
           ..\..\..\..\lib\BdaSup.lib
```

<a href="" id="--------includes---"></a> 包括   
指向要搜索的 BDA 驱动程序的示例源需要为了编译的头文件的路径的列表。 下面的代码提供了一个示例：

```make
INCLUDES=..\..\..\..\inc; \
    $(DDK_INC_PATH)\wdm; 
```

<a href="" id="--------sources-------"></a> 源   
指向必须进行编译，生成该驱动程序的源文件的列表。 文件必须位于在其中的目录*源*文件所在的。 下面的代码提供了一个示例：

```make
SOURCES= \
    ObjDesc.cpp     \
    inpin.cpp     \
    outpin.cpp    \
    Filter.cpp      \
    Device.cpp      \
    bdaguid.c       \
    BDAsampl.rc
```

<a href="" id="--------drivertype-------"></a> DRIVERTYPE   
将驱动程序的类型设置为 WDM，如下面的代码中所示：

```make
DRIVERTYPE=WDM
```

<a href="" id="--------use-mapsym-------"></a> USE\_MAPSYM   
生成 *.sym*符号文件，除了 *.pdb*符号文件。 这些文件将名称映射到地址。 设置此宏需要在 Windows 98 上进行调试 / 我的平台。 将此宏设置下面的示例中所示：

```make
USE_MAPSYM=1
```
