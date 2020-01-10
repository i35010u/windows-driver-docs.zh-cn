---
title: Stampinf 命令选项
description: Stampinf 是一个命令行工具，可更新常见的 INF 文件指令。
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
ms.openlocfilehash: f0bb394ca77654a333863aff92163b3d9a261633
ms.sourcegitcommit: b06bf47dca21779d4cbcaf43d7485815aa2a35fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75737606"
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


<span id="_______-f________filename______"></span><span id="_______-F________FILENAME______"></span> **-f** *filename*   
指定要处理的 INF 或 INX 文件。

<span id="-s_section"></span><span id="-S_SECTION"></span> **-s** *部分*  
指定要在其中放置 [**INF DriverVer 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)的 INF 部分。 此指令所在的默认位置是 [**INF Version 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)。

<span id="_______-d_________date_____"></span><span id="_______-D_________DATE_____"></span> **-d** \[*日期* |  **\\** <em>\]  
指定在[INF DriverVer 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)中写入的日期。 日期的格式为 "月/日/年</em> （例如， **-d 10/20/2011**）。

若要使用当前日期，请使用此参数指定星号（\*）。

如果未指定 **-d**参数，或未指定任何选项，Stampinf 将使用以下日期值之一：

-   如果设置了 STAMPINF\_日期环境变量，则 Stampinf 将使用此环境变量指定的日期值。

-   如果未指定 STAMPINF\_DATE 环境变量，则 Stampinf 将使用当前日期。

<span id="_______-a_________architecture______________"></span><span id="_______-A_________ARCHITECTURE______________"></span> **-\[** *体系结构* **\]**    
指定 *architecture* 字符串来替换 INX 文件中使用的 $ARCH$ 变量。 $ARCH $ 变量用于自定义[**INF 制造商部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)的**TargetOSVersion**装饰，并将其相应的部分名称自定义到特定平台。 有关 $ARCH $ 变量的详细信息，请参阅[使用 INX 文件创建 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)。

*体系结构*字符串的值为**x86**、 **64** （对于基于 Itanium 的平台）和**x64** （适用于 amd64 平台）。

如果未指定 **-a**参数或未指定任何选项，则 Stampinf 将使用平台环境变量指定的值，该变量是在生成环境窗口中设置的。

<span id="_______-c________catalogfile______"></span><span id="_______-C________CATALOGFILE______"></span> **-c** *catalogfile*   
指定在 [**INF Version 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)中的 **CatalogFile** 指令中写入的值。 默认情况下不写入 **CatalogFile** 指令。

<span id="_______-v_________time_____"></span><span id="_______-V_________TIME_____"></span> **-v \[** *时间* **| \*\]**  
指定在版本号的 [**INF DriverVer 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)中写入的时间。 时间格式为 *hours.minutes.seconds.milliseconds*（例如，11.30.20.15）。 此选项在开发过程中非常有用，因为通过它可以方便地提高驱动程序的版本号。

若要使用当前时间，请在此参数中指定星号 (\*)。

如果未指定 **-v**参数或未指定任何选项，Stampinf 将使用以下版本号值之一：

-   如果设置了 STAMPINF\_版本环境变量，则 Stampinf 将使用此环境变量指定的版本号值。

-   如果未指定 STAMPINF\_版本环境变量，则 Stampinf 将从 Ntverp.h 后文件中提取版本号。

<span id="_______-k________version______"></span><span id="_______-K________VERSION______"></span> **-k** *版本*   
指定此驱动程序所依赖的 KMDF 的*版本*。 这用于自定义 INF 文件中的 KmdfLibraryVersion 和 KMDF 辅助安装程序的名称。 此选项取代了 INF 文件中的 $KMDFVERSION$ 和 $KMDFCOINSTALLERVERSION$ 关键字。 该字符串采用以下格式：

*&lt;主要\_版本&gt;。&lt;次要\_版本&gt;*

例如，如果你将 1.5 指定为版本字符串，则两个关键字将分别使用值 1.5 和 01005。

<span id="_______-u________version______"></span><span id="_______-U________VERSION______"></span> **-u** *版本*   
指定此驱动程序依赖的 UMDF 的版本。 此选项用于指定 INF 文件中的 UmdfLibraryVersion 和 UMDF 辅助安装程序的名称。 指定的版本 将取代 INF 文件中的 $UMDFVERSION$ 和 $UMDFCOINSTALLERVERSION$ 关键字。 *版本*字符串具有以下格式：

*&lt;主要\_版本&gt;* 。 *&lt;次要\_版本&gt;* 。 *&lt;service\_版本&gt;*

（其中 *&lt;服务\_版本&gt;* 通常为零）。

例如，如果你将 1.5.0 指定为版本字符串，则最大和最小关键字将分别使用值 1.5.0 和 01005。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
显示详细的 Stampinf 输出。

<span id="-i_path"></span><span id="-I_PATH"></span> **-i** *路径*  
指定 Ntverp.h 后文件的位置。 *路径*表示包含 ntverp.h 后的目录的完全限定位置。

### <a name="comments"></a>说明

Stampinf 放入[**INF DriverVer 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)中的日期值不是基于协调世界*时*（UTC），也称为*格林尼治标准时间*。 但是， [**Inf2Cat**](inf2cat.md)会将此 INF 指令的日期值解释为 UTC 值。 如果 Stampinf 使用的本地日期值被 Inf2Cat 解释为明天日期的 UTC 值，这可能会导致错误。 若要避免此问题，请执行以下操作*之一*：

-   将 STAMPINF\_DATE 环境变量设置为相应的 UTC 日期值。 现在无需指定 **-d**参数即可运行 Stampinf。 这会指示 Stampinf 使用 STAMPINF\_DATE 环境变量指定的日期值。  现在，Stampinf 和 Inf2Cat 都使用 UTC。
-   更改驱动程序包项目设置，使 Inf2Cat `/uselocaltime`设置。 为此，请使用“配置属性”->“Inf2Cat”->“常规”->“使用本地时间”。 现在，Stampinf 和 Inf2Cat 都使用本地时间。

开发驱动程序时，可以将环境变量 PRIVATE\_驱动程序\_包。 设置此变量后，Stampinf 会将用于[**INF DriverVer 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)的日期和版本设置为当前日期和时间，而不考虑命令行设置。 此外，Stampinf 还设置了**CatalogFile**指令。 Stampinf 在[**INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)写入**CatalogFile = delta** ，除非已使用 **-c**命令选项指定了目录。

在生成窗口中键入以下命令，以启用此开发模式：

```
set PRIVATE_DRIVER_PACKAGE=1
```

 

 





