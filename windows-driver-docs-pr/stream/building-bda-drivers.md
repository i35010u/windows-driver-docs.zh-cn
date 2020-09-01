---
title: 生成 BDA 驱动程序
description: 生成 BDA 驱动程序
ms.assetid: 2272fa18-5102-443e-8728-f256444ab044
keywords:
- 广播驱动程序体系结构 WDK AVStream，构建驱动程序
- BDA WDK AVStream，构建驱动程序
- 构建驱动程序 WDK，BDA
- 生成实用工具 WDK，BDA
- 宏 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 486f2e4d8617ff99e2c711bf6b1ba300e94a9b35
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186387"
---
# <a name="building-bda-drivers"></a>生成 BDA 驱动程序





**注意**   从 Windows 8 开始，WDK 构建环境不再使用 Build.exe。 请参阅 [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)。 以下讨论仅适用于使用 WDK Windows 7 版本或更早版本构建驱动程序的情况。

 

您可以使用 Microsoft Windows 驱动程序工具包 (WDK) 来构建 (BDA) 驱动程序的广播驱动程序体系结构。 若要构建 BDA 驱动程序，请打开 WDK 构建环境窗口，将其更改为 WDK 的主源目录的相应的 BDA 驱动程序源代码子目录，并使用 " **生成** " 命令。 " **生成** " 命令获取有关如何从驻留在 "bda 驱动程序" 源代码子目录中的 *源* 文件生成 BDA 驱动程序的说明。

有关生成实用工具、WDK 的生成环境、用于控制生成实用工具的宏和环境变量，以及生成 BDA 驱动程序所需的文件的详细信息，请参阅 Windows 7 WDK 文档中的 "使用生成实用工具" 和 "生成实用工具参考" (生成 7600) 。

下面的列表包含在 BDA *源* 文件中使用的宏名称，并讨论如何使用它们来构建 BDA 驱动程序：

<a href="" id="--------targetname-------"></a> TARGETNAME   
设置为 BDA 驱动程序的名称，以便在 WDK 构建驱动程序时，它是用此名称生成的。 以下代码提供了一个示例：

```make
TARGETNAME=BDAsampl  # WDK builds the driver as BDAsampl.sys
```

<a href="" id="--------targetpath-------"></a> TARGETPATH   
设置生成的驱动程序的目标目录。 请注意，根据您的生成环境是 "免费" 还是 "已选中"，可以使用 "生成" \_ ALT \_ 目录变量将 "如 fre" 或 ".chk" 追加到 \\ 生成命令在包含 *源文件* 的目录下创建的 obj 子目录中。 以下代码提供了一个示例：

```make
TARGETPATH=obj$(BUILD_ALT_DIR) # built driver in \objfre or \objchk
```

<a href="" id="--------targettype-------"></a> TARGETTYPE   
将 "要生成的文件类型" 设置为 "驱动程序" (而不是，例如程序或 DLL) 如以下代码所示：

```make
TARGETTYPE=DRIVER  # WDK builds the driver as *.sys
```

<a href="" id="--------targetlibs-------"></a> TARGETLIBS   
指向该 BDA 驱动程序的示例源必须链接到的库文件。 一个 BDA 驱动程序必须至少链接到下面的代码示例中所示的库：

```make
TARGETLIBS=..\..\..\..\lib\ks.lib \
           ..\..\..\..\lib\ksguid.lib \
           ..\..\..\..\lib\BdaSup.lib
```

<a href="" id="--------includes---"></a> 涵盖   
指向一个路径列表，搜索该 BDA 驱动程序的示例所需的标头文件以进行编译。 以下代码提供了一个示例：

```make
INCLUDES=..\..\..\..\inc; \
    $(DDK_INC_PATH)\wdm; 
```

<a href="" id="--------sources-------"></a> 渠道   
指向必须编译才能生成驱动程序的源文件的列表。 文件必须 *位于源文件所在* 的目录中。 以下代码提供了一个示例：

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
将驱动程序的类型设置为 WDM，如以下代码所示：

```make
DRIVERTYPE=WDM
```

<a href="" id="--------use-mapsym-------"></a> 使用 \_ MAPSYM   
除了 *.pdb*符号文件外，还会生成*符号*符号文件。 这些文件将名称映射到地址。 需要设置此宏才能在 Windows 98/Me 平台上进行调试。 设置此宏，如下面的示例中所示：

```make
USE_MAPSYM=1
```