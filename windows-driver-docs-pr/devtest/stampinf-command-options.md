---
title: Stampinf 命令选项
description: Stampinf 是更新通用 INF 文件指令的命令行工具。
ms.assetid: 409b1bcc-9e19-4a95-a459-fc9f1ec41ea1
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
ms.openlocfilehash: 762cfeac2a7e723a7cc02c0fb3f672677e0006fc
ms.sourcegitcommit: e123b8b69473c0ebc0383ef722452866bf6662d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66394272"
---
# <a name="stampinf-command-options"></a>Stampinf 命令选项


Stampinf 是更新通用 INF 文件指令的命令行工具。

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-f________filename______"></span><span id="_______-F________FILENAME______"></span> **-f** *filename*   
指定要处理的 INF 或 INX 文件。

<span id="-s_section"></span><span id="-S_SECTION"></span> **-s** *section*  
指定要在其中放置 [**INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)的 INF 部分。 此指令所在的默认位置是 [**INF Version 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)。

<span id="_______-d_________date_____"></span><span id="_______-D_________DATE_____"></span> **-d** \[ *date* |  **\\** <em>\]  
指定在编写的日期 [</em>*INF DriverVer 指令*<em>](https://msdn.microsoft.com/library/windows/hardware/ff547394)。为日期格式是*月</em>/* 日期 */* 年 * (例如， **-d 2011 年 10 月 20 日**)。

若要使用当前日期，请指定一个星号 (\*) 使用此参数。

如果 **-d**参数未指定，或使用，则指定不带任何选项，Stampinf 以下日期值之一：

-   如果 STAMPINF\_设置日期的环境变量，Stampinf 将使用此环境变量指定的日期值。

-   如果 STAMPINF\_未指定日期的环境变量，Stampinf 使用当前日期。

<span id="_______-a_________architecture______________"></span><span id="_______-A_________ARCHITECTURE______________"></span> **-a \[** *architecture* **\]**    
指定 *architecture* 字符串来替换 INX 文件中使用的 $ARCH$ 变量。 $ARCH$ 变量用于自定义**TargetOSVersion**中的修饰[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)，及其相应的节名称，为特定平台。 有关 $ARCH$ 变量的详细信息，请参阅[使用 INX 文件转换为创建 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff545473)。

值*体系结构*的字符串是否**x86**， **64** （适用于基于 Itanium 的平台），以及**x64** （适用于 amd64 平台）。

如果 **-a**参数未指定或指定不带任何选项，则 Stampinf 使用指定的生成环境窗口中设置的平台环境变量的值。

<span id="_______-c________catalogfile______"></span><span id="_______-C________CATALOGFILE______"></span> **-c** *catalogfile*   
指定在 [**INF Version 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)中的 **CatalogFile** 指令中写入的值。 默认情况下，未编写 **CatalogFile** 指令。

<span id="_______-v_________time_____"></span><span id="_______-V_________TIME_____"></span> **-v \[** *time* **| \*\]**  
指定在版本号的 [**INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)中写入的时间。 时间格式为 *hours.minutes.seconds.milliseconds*（例如，11.30.20.15）。 此选项在开发过程中非常有用，因为通过它可以方便地提高驱动程序的版本号。

若要使用当前时间，请在此参数中指定星号 (\*)。

如果 **-v**参数未指定或指定不带任何选项，Stampinf 使用以下的版本编号值之一：

-   如果 STAMPINF\_设置版本的环境变量，Stampinf 将使用此环境变量指定的版本编号值。

-   如果 STAMPINF\_未指定版本的环境变量，Stampinf 从 Ntverp.hNtverp.h 文件中提取的版本号。

<span id="_______-k________version______"></span><span id="_______-K________VERSION______"></span> **-k** *version*   
指定*版本*的 KMDF 取决于此驱动程序。 这用于自定义 INF 文件中的 KmdfLibraryVersion 和 KMDF 辅助安装程序的名称。 此选项取代了 INF 文件中的 $KMDFVERSION$ 和 $KMDFCOINSTALLERVERSION$ 关键字。 该字符串采用以下格式：

*&lt;主要\_版本&gt;。&lt;次要\_版本&gt;*

例如，如果你将 1.5 指定为版本字符串，则两个关键字将分别使用值 1.5 和 01005。

<span id="_______-u________version______"></span><span id="_______-U________VERSION______"></span> **-u** *version*   
指定此驱动程序依赖的 UMDF 的*版本*。 此选项用于指定 INF 文件中的 UmdfLibraryVersion 和 UMDF 辅助安装程序的名称。 指定的 *version* 将取代 INF 文件中的 $UMDFVERSION$ 和 $UMDFCOINSTALLERVERSION$ 关键字。 *版本*字符串具有采用以下格式：

*&lt;主要\_版本&gt;* 。 *&lt;次要\_版本&gt;* 。 *&lt;服务\_版本&gt;*

(其中 *&lt;服务\_版本&gt;* 通常为零)。

例如，如果你将 1.5.0 指定为版本字符串，则最大和最小关键字将分别使用值 1.5.0 和 01005。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
显示详细 Stampinf 输出。

<span id="-i_path"></span><span id="-I_PATH"></span> **-i** *path*  
指定 ntverp.h 后文件的位置。 *路径*表示包含 ntverp.h 后的目录的完全限定的位置

### <a name="comments"></a>备注

Stampinf 将放入中的日期值[ **INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)不基于*协调世界时*(UTC)，这是也称为*格林威治标准时间*。 但是， [ **Inf2Cat** ](inf2cat.md)将解释为 UTC 值此 INF 指令的日期值。 如果由 Stampinf 的本地日期值解释 Inf2Cat 为 UTC 值为将来的日期，这可能导致错误。 若要避免此问题，请执行*一个*以下值：

-   设置 STAMPINF\_日期为适当的 UTC 日期值的环境变量。 现在，而无需指定运行 Stampinf **-d**参数。 这会指示 Stampinf 使用 STAMPINF 由指定的日期值\_日期环境变量。  现在 Stampinf 和 Inf2Cat 使用 UTC。
-   更改驱动程序程序包项目设置以便 Inf2Cat 设置`/uselocaltime`。 为此，请使用  “配置属性”->“Inf2Cat”->“常规”->“使用本地时间”。 现在 Stampinf 和 Inf2Cat 使用本地时间。

当开发您的驱动程序时，您可以设置环境变量私有\_驱动程序\_包。 Stampinf 时设置此变量，设置的日期和所用的版本[ **INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)为当前日期和时间，而不考虑命令行设置。 此外，设置 Stampinf **CatalogFile**指令。 将写入 Stampinf **CatalogFile=delta.cat**中[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)，除非使用已指定目录 **-c**命令选项。

若要启用此开发模式生成窗口中键入以下命令：

```
set PRIVATE_DRIVER_PACKAGE=1
```

 

 





