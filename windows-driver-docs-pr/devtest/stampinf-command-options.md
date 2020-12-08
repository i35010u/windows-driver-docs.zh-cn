---
title: Stampinf 命令选项
description: Stampinf 是一个命令行工具，可更新常见的 INF 文件指令。
keywords:
- Stampinf 命令选项驱动程序开发工具
topic_type:
- apiref
api_name:
- Stampinf
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74d6a1db2543484cfc850dc05d9419e4d523cb63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826669"
---
# <a name="stampinf-command-options"></a>Stampinf 命令选项


Stampinf 是一个命令行工具，可更新常见的 INF 文件指令。

```
Stampinf -f filename 
[-s section] 
[-d [date | *]] 
[-a [architecture]] 
[-c catalogfile]
[-v [time | *]]
[-k version] 
[-u version]
[-i path]
[-n]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-f________filename______"></span><span id="_______-F________FILENAME______"></span>**-f** *filename*   
指定要处理的 INF 或 INX 文件。

<span id="-s_section"></span><span id="-S_SECTION"></span>**-s** *部分*  
指定要在其中放置 [**INF DriverVer 指令**](../install/inf-driverver-directive.md)的 INF 部分。 此指令所在的默认位置是 [**INF Version 部分**](../install/inf-version-section.md)。

<span id="_______-d_________date_____"></span><span id="_______-D_________DATE_____"></span>**-d** \[*日期* | **\\**<em>\]  
指定在 [INF DriverVer 指令](../install/inf-driverver-directive.md)中写入的日期。 日期的格式为月/日/年 </em> (例如， **-d 10/20/2011**) 。

若要使用当前日期，请在此参数中指定星号 (\*)。

如果未指定 **-d** 参数，或未指定任何选项，Stampinf 将使用以下日期值之一：

-   如果设置了 STAMPINF \_ DATE 环境变量，则 STAMPINF 将使用此环境变量指定的日期值。

-   如果 \_ 未指定 STAMPINF date 环境变量，则 STAMPINF 将使用当前日期。

<span id="_______-a_________architecture______________"></span><span id="_______-A_________ARCHITECTURE______________"></span>**-a \[***体系结构***\]**   
指定 *architecture* 字符串来替换 INX 文件中使用的 $ARCH$ 变量。 $ARCH $ 变量用于自定义 [**INF 制造商部分**](../install/inf-manufacturer-section.md)的 **TargetOSVersion** 装饰，并将其相应的部分名称自定义到特定平台。 有关 $ARCH $ 变量的详细信息，请参阅 [使用 INX 文件创建 INF 文件](../wdf/using-inx-files-to-create-inf-files.md)。

*体系结构* 字符串的值为 **x86**、 **64** (，适用于基于 Itanium 的平台) 和适用于 amd64 平台的 **x64** () 。

如果未指定 **-a** 参数或未指定任何选项，则 Stampinf 将使用平台环境变量指定的值，该变量是在生成环境窗口中设置的。

<span id="_______-c________catalogfile______"></span><span id="_______-C________CATALOGFILE______"></span>**-c** *catalogfile*   
指定在 [**INF Version 部分**](../install/inf-version-section.md)中的 **CatalogFile** 指令中写入的值。 默认情况下不写入 **CatalogFile** 指令。

<span id="_______-v_________time_____"></span><span id="_______-V_________TIME_____"></span>**-v \[***时间***| \*\]**  
指定在版本号的 [**INF DriverVer 指令**](../install/inf-driverver-directive.md)中写入的时间。 时间格式为 *hours.minutes.seconds.milliseconds*（例如，11.30.20.15）。 此选项在开发过程中非常有用，因为通过它可以方便地提高驱动程序的版本号。

若要使用当前时间，请在此参数中指定星号 (\*)。

如果未指定 **-v** 参数或未指定任何选项，Stampinf 将使用以下版本号值之一：

-   如果设置了 STAMPINF \_ 版本环境变量，则 STAMPINF 将使用此环境变量指定的版本号值。

-   如果 \_ 未指定 STAMPINF 版本环境变量，则 STAMPINF 将从 ntverp.h 后文件中提取版本号。

<span id="_______-k________version______"></span><span id="_______-K________VERSION______"></span>**-k** *版本*   
指定此驱动程序所依赖的 KMDF 的 *版本* 。 这用于自定义 INF 文件中的 KmdfLibraryVersion 和 KMDF 辅助安装程序的名称。 此选项取代了 INF 文件中的 $KMDFVERSION$ 和 $KMDFCOINSTALLERVERSION$ 关键字。 该字符串采用以下格式：

*&lt;主要 \_ 版本 &gt; 。 &lt;次 \_ 版本&gt;*

例如，如果你将 1.5 指定为版本字符串，则两个关键字将分别使用值 1.5 和 01005。

<span id="_______-u________version______"></span><span id="_______-U________VERSION______"></span>**-u** *版本*   
指定此驱动程序依赖的 UMDF 的版本。 此选项用于指定 INF 文件中的 UmdfLibraryVersion 和 UMDF 辅助安装程序的名称。 指定的版本 将取代 INF 文件中的 $UMDFVERSION$ 和 $UMDFCOINSTALLERVERSION$ 关键字。 *版本* 字符串具有以下格式：

*&lt; 主要 \_ 版本 &gt;**。 &lt;次 \_ 版本 &gt;**。 &lt;服务 \_ 版本 &gt;*

 (，其中 *&lt; 服务 \_ 版本 &gt;* 通常为零) 。

例如，如果你将 1.5.0 指定为版本字符串，则最大和最小关键字将分别使用值 1.5.0 和 01005。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
显示详细的 Stampinf 输出。

<span id="-i_path"></span><span id="-I_PATH"></span>**-i** *路径*  
指定 Ntverp.h 后文件的位置。 *路径* 表示包含 ntverp.h 后的目录的完全限定位置。

### <a name="comments"></a>注释

Stampinf 放入 [**INF DriverVer 指令**](../install/inf-driverver-directive.md) 中的日期值不基于 *协调世界时* ， (UTC) ，也称为 *格林尼治标准时间*。 但是， [**Inf2Cat**](inf2cat.md) 会将此 INF 指令的日期值解释为 UTC 值。 如果 Stampinf 使用的本地日期值被 Inf2Cat 解释为明天日期的 UTC 值，这可能会导致错误。 若要避免此问题，请执行以下操作 *之一* ：

-   将 STAMPINF \_ date 环境变量设置为相应的 UTC 日期值。 现在无需指定 **-d** 参数即可运行 Stampinf。 这会指示 Stampinf 使用由 STAMPINF date 环境变量指定的日期值 \_ 。  现在，Stampinf 和 Inf2Cat 都使用 UTC。
-   更改驱动程序包项目设置，使 Inf2Cat 设置 `/uselocaltime` 。 为此，请使用“配置属性”->“Inf2Cat”->“常规”->“使用本地时间”。 现在，Stampinf 和 Inf2Cat 都使用本地时间。

开发驱动程序时，可以设置环境变量私有 \_ 驱动 \_ 程序包。 设置此变量后，Stampinf 会将用于 [**INF DriverVer 指令**](../install/inf-driverver-directive.md) 的日期和版本设置为当前日期和时间，而不考虑命令行设置。 此外，Stampinf 还设置了 **CatalogFile** 指令。 Stampinf 在 [**INF 版本部分**](../install/inf-version-section.md)写入 **CatalogFile = delta** ，除非已使用 **-c** 命令选项指定了目录。

在生成窗口中键入以下命令，以启用此开发模式：

```
set PRIVATE_DRIVER_PACKAGE=1
```

 

