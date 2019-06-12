---
title: 监视器 INF 文件部分
description: 监视器 INF 文件部分
ms.assetid: f5208b6a-00b0-446e-82f7-eb26082ed9a5
keywords:
- 监视 INF 文件部分 WDK Windows 2000 显示
- INF 文件 WDK Windows 2000 显示
- INF 编写器定义的各节 WDK Windows 2000 显示
- DDInstall 部分 WDK Windows 2000 显示
- 模型部分 WDK Windows 2000 显示
- SourceDisksFiles 部分 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be80268e6a106f6e9118d3d1274137288d6c8c10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542658"
---
# <a name="monitor-inf-file-sections"></a>监视器 INF 文件部分


## <span id="ddk_monitor_inf_file_sections_gg"></span><span id="DDK_MONITOR_INF_FILE_SECTIONS_GG"></span>


监视器必须安装在基于 NT 的操作系统使用 INF 文件。 Windows Driver Kit (WDK) 提供了示例监视器 INF 文件*monsamp.inf*，是应使用作为模板来为你的监视器生成的 INF 文件。 不能使用*geninf.exe*工具中所述[创建图形 INF 文件](creating-graphics-inf-files.md)生成监视器 INF。

本主题的其余部分上的某些部分中的注释*monsamp.inf*的监视器 INF 编写器特别感兴趣的是。 INF 文件有关的更多常规信息，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

INF 文件还可用于替代监视器扩展显示标识数据 (EDID)。 请参阅[重写使用 INF 监视器 EDIDs](overriding-monitor-edids.md)。

### <a name="span-idsourcedisksfilessectionspanspan-idsourcedisksfilessectionspanspan-idsourcedisksfilessectionspansourcedisksfiles-section"></a><span id="SourceDisksFiles_Section"></span><span id="sourcedisksfiles_section"></span><span id="SOURCEDISKSFILES_SECTION"></span>SourceDisksFiles 部分

必须在监视安装过程中复制的文件应置于 **\[SourceDisksFiles\]** 部分。 下面的示例标识。*icm*分发磁盘 1 上的文件。

```inf
[SourceDisksFiles]
profile1.icm=1
```

有关更多常规信息，请参阅[ **INF SourceDisksFiles 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547472)。 请参阅[监视配置文件](monitor-profiles.md)有关颜色管理和配置文件的详细信息。

### <a name="span-idmodelssectionspanspan-idmodelssectionspanspan-idmodelssectionspanmodels-section"></a><span id="Models_Section"></span><span id="models_section"></span><span id="MODELS_SECTION"></span>模型部分

有关给定制造商支持每个模型的信息应置于*模型*部分。 下面的示例标识由 ACME 生产的两个模型：

```inf
[ACME]
%ACME-1234%=ACME-1234.Install, Monitor\MON12AB
%ACME-5678%=ACME-5678.Install, Monitor\MON34CD
```

每个模型表示由单个线条。 每个行包含三个元素：

-   模型名称-例如， **%%acme-1234年**是一个标记，用于表示实际模型名称 (这将显示在**字符串**部分)。

-   链接到后续*DDInstall*部分-例如， **ACME 1234。安装**有一个指向后续 **\[ACME 1234。安装\]** 部分。

-   硬件标识-例如，表达式**监视器\\MON12AB**出现在设备的组合的设备类 （监视器） 和设备标识 (MON12AB) *EDID*.

有关更多常规信息，请参阅[ **INF 模型部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)。

### <a name="span-idddinstallsectionspanspan-idddinstallsectionspanspan-idddinstallsectionspanddinstall-section"></a><span id="DDInstall_Section"></span><span id="ddinstall_section"></span><span id="DDINSTALL_SECTION"></span>DDInstall 部分

*DDInstall*部分提供有关安装指定的设备时要执行的操作向驱动程序的信息。 本部分中的每一行提供链接或为不同 INF 编写器定义的分区的更高版本出现在 INF 文件的链接。 下面的示例演示*DDInstall* ACME 1234 模型的部分：

```inf
[ACME-1234.Install]
DelReg=DEL_CURRENT_REG
AddReg=ACME-1234.AddReg, 1280, DPMS
CopyFiles=ACME-1234.CopyFiles
```

-   [**DelReg** ](https://msdn.microsoft.com/library/windows/hardware/ff547374)指令-提供了指向**DEL\_当前\_REG**部分中，它详细说明了要删除的注册表项。

-   [**AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)指令-提供了三个部分的链接的注册表中详细介绍要添加的键。 这些章节**ACME 1234。AddReg**， **1280年**，和**DPMS**。

-   [**CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)指令-提供了指向**ACME 1234。CopyFiles**部分中，它指定要从分发磁盘或磁盘复制的文件。

有关更多常规信息，请参阅[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)。

### <a name="span-idinfwriter-definedsectionsspanspan-idinfwriter-definedsectionsspanspan-idinfwriter-definedsectionsspaninf-writer-defined-sections"></a><span id="INF_Writer-Defined_Sections"></span><span id="inf_writer-defined_sections"></span><span id="INF_WRITER-DEFINED_SECTIONS"></span>INF 编写器定义部分

INF 编写器定义的部分可以具有任何名称，前提是该 INF 文件中唯一。 这些部分所指向的其他部分中的指令。 以下项目符号项讨论的某些 INF 编写器定义部分从*monsamp.inf*:

-   **DEL\_当前\_REG**部分-标识其值将被删除的四个注册表项：**模式**， **MaxResolution**， **DPMS**，并且**ICMProfile**。 将后续部分中的新值与相应地更新这些密钥。

    ```inf
    [DEL_CURRENT_REG]
    HKR,MODES
    HKR,,MaxResolution
    HKR,,DPMS
    HKR,,ICMProfile
    ```

-   **1280**部分-更新**MaxResolution**到显示的字符串值的注册表项。

    ```inf
    [1280]
    HKR,,MaxResolution,,"1280, 1024"
    ```

-   **DPMS**部分-更新**DPMS**为 1 (TRUE) 的注册表项。 对于不支持电源管理的监视器，以下行应改为设**DPMS**密钥值为 0 (FALSE)。

    ```inf
    [DPMS]
    HKR,,DPMS,,1
    ```

-   **AddReg**)。 因此，**模式**EDID 或 EDID 解释存在问题时，才应使用 INF 键值。

    为每个子**模式**密钥指定分辨率，并且可以包含用来指定特定时间或时间范围的最多九个值。 对于每个子项的名称解析必须是两个整数值-宽度和高度-用逗号分隔的组合。 从名为特定的计时**1>** 到**Mode9**。 命名必须是连续的。 字符串值允许水平和垂直同步波作为单个值或范围，其中一个范围指定为最小值，必须指定的频率后跟短划线 （-） 后, 跟最大值。 当前仅作为整数，其后面忽略小数位的任何数字解释频率值。 字符串允许水平和垂直同步脉冲指定的极性。 但是，当前忽略这些极性值。 每个字符串中需要最大水平同步的脉冲值。 例如，下面的演示，对于每个子项的字符串，用方括号括起来的信息是可选的：

    ```inf
    [{MinHSync}-]{MaxHSync}[,{MinVSync}-{MaxVSynx}] 
    ```

    因此，每个子项的字符串可以指定而无需垂直同步范围。 但是，不建议指定一个子项的字符串，而无需垂直同步范围。

    下面的设置的第一行 **"模式\\1280,1024"** 子项显示的字符串值。 在同一行还标识此子项的值名称**模式 1**。 第一对字符串以下中的数字**模式 1**子项指定的水平的同步频率的范围单位为 KHz。 此字符串中的数字的下一步对指定垂直同步频率，的范围中 Hz。 在第二个行中， **PreferredMode**注册表项设置为在随附的字符串中显示的值。 在字符串中的值用于为首选的屏幕模式中像素和屏幕刷新频率，设置水平和垂直分辨率，赫兹 (Hz) 中。 仅水平滚动条和垂直分辨率值中所需**PreferredMode**字符串。 例如，下面显示了，对于**PreferredMode**用方括号括起来的信息是可选的字符串：

    ```inf
    {Width},{Height}[,{Frequency}]
    ```

    因此，可以不以频率指定首选的模式。 但是，建议不要指定不带频率为首选的模式。

    第三个行集**ICMProfile**密钥对的字符串值 **"profile1.icm"** 。

    ```inf
    [ACME-1234.AddReg]
    HKR,"MODES\1280,1024",Mode1,,"27.0-106.0,55.0-160.0,+,+"
    HKR,,PreferredMode,,"1024,768,70"
    HKR,,ICMProfile,0,"profile1.icm"
    ```

    对于满足 sRGB 规范，这是首选，监视器需要没有监视器的配置文件。

