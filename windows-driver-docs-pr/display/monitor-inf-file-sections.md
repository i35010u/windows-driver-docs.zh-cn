---
title: 监视 INF 文件节
description: 监视 INF 文件节
keywords:
- 监视 INF 文件部分 WDK Windows 2000 显示
- INF 文件 WDK Windows 2000 显示
- INF Windows 2000 显示的 INF 写入方定义的部分
- DDInstall 部分 WDK Windows 2000 显示
- "\"模型\" 部分 WDK Windows 2000 显示"
- SourceDisksFiles 部分 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d1abb89dd36ccc2aac52d292ca5ccbc08ee415d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840389"
---
# <a name="monitor-inf-file-sections"></a>监视 INF 文件节


## <span id="ddk_monitor_inf_file_sections_gg"></span><span id="DDK_MONITOR_INF_FILE_SECTIONS_GG"></span>


必须使用 INF 文件在基于 NT 的操作系统上安装监视器。 Windows 驱动程序工具包 (WDK) 提供一个示例监视器 INF 文件 *monsamp*，您应将该文件用作模板，以便为您的监视器生成 INF 文件。 不能使用 [创建图形 Inf 文件](creating-graphics-inf-files.md)中介绍的 *geninf.exe* 工具来生成监视器 inf。

本主题的其余部分将对 *monsamp* 中特定于监视 inf 编写器感兴趣的部分进行评论。 有关 INF 文件的更多常规信息，请参阅 [Inf 文件部分和指令](../install/index.md)。

你还可以使用 INF 文件来替代监视 (EDID) 的扩展显示标识数据。 请参阅 [使用 INF 替代监视器 edid](overriding-monitor-edids.md)。

### <a name="span-idsourcedisksfiles_sectionspanspan-idsourcedisksfiles_sectionspanspan-idsourcedisksfiles_sectionspansourcedisksfiles-section"></a><span id="SourceDisksFiles_Section"></span><span id="sourcedisksfiles_section"></span><span id="SOURCEDISKSFILES_SECTION"></span>SourceDisksFiles 部分

在监视器安装过程中必须复制的文件应放置在 **\[ SourceDisksFiles \]** 节中。 下面的示例标识一个。分发磁盘1上的 *icm* 文件。

```inf
[SourceDisksFiles]
profile1.icm=1
```

有关更多常规信息，请参阅 [**INF SourceDisksFiles 部分**](../install/inf-sourcedisksfiles-section.md)。 有关颜色管理和配置文件的详细信息，请参阅 [监视配置文件](monitor-profiles.md) 。

### <a name="span-idmodels_sectionspanspan-idmodels_sectionspanspan-idmodels_sectionspanmodels-section"></a><span id="Models_Section"></span><span id="models_section"></span><span id="MODELS_SECTION"></span>模型部分

有关给定制造商支持的每个模型的信息应放置在 " *模型* " 部分中。 下面的示例标识由 ACME 制造的两个模型：

```inf
[ACME]
%ACME-1234%=ACME-1234.Install, Monitor\MON12AB
%ACME-5678%=ACME-5678.Install, Monitor\MON34CD
```

每个模型由单个行表示。 每行包含三个元素：

-   模型名称--例如， **% ACME-1234%** 是一个标记，它表示将在) 的 **字符串** 部分显示的实际模型名称 (。

-   链接到后续的 *DDInstall* 部分，例如 **ACME-1234。安装** 是指向后续 **\[ ACME-1234 的链接。安装 \]** 部分。

-   硬件标识--例如，表达式 **监视器 \\ MON12AB** 将设备类 (监视器) 和设备标识 (MON12AB) 与设备 *EDID* 中显示的相同。

有关更多常规信息，请参阅 [**INF 模型部分**](../install/inf-models-section.md)。

### <a name="span-idddinstall_sectionspanspan-idddinstall_sectionspanspan-idddinstall_sectionspanddinstall-section"></a><span id="DDInstall_Section"></span><span id="ddinstall_section"></span><span id="DDINSTALL_SECTION"></span>DDInstall 部分

*DDInstall* 部分为驱动程序提供有关在安装指定设备时要执行的操作的信息。 本部分中的每行都提供一个链接，或指向 INF 文件中稍后显示的不同 INF 编写器定义的部分的链接。 下面的示例显示了 ACME-1234 模型的 *DDInstall* 部分：

```inf
[ACME-1234.Install]
DelReg=DEL_CURRENT_REG
AddReg=ACME-1234.AddReg, 1280, DPMS
CopyFiles=ACME-1234.CopyFiles
```

-   [**DelReg**](../install/inf-delreg-directive.md) 指令-提供指向 **DEL \_ 当前 \_ REG** 部分的链接，该链接详细说明了要删除的注册表项。

-   [**AddReg**](../install/inf-addreg-directive.md) 指令-提供指向三个部分的链接，其中包含要添加的注册表项。 这些部分为 **ACME-1234。AddReg**、 **1280** 和 **DPMS**。

-   [**CopyFiles**](../install/inf-copyfiles-directive.md) 指令-提供指向 **ACME-1234 的链接。CopyFiles** 部分，指定要从分发磁盘复制的文件。

有关更多常规信息，请参阅 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)。

### <a name="span-idinf_writer-defined_sectionsspanspan-idinf_writer-defined_sectionsspanspan-idinf_writer-defined_sectionsspaninf-writer-defined-sections"></a><span id="INF_Writer-Defined_Sections"></span><span id="inf_writer-defined_sections"></span><span id="INF_WRITER-DEFINED_SECTIONS"></span>INF Writer-Defined 节

INF 写入方定义的节可以具有任何名称，前提是它在 INF 文件中是唯一的。 这些部分由其他部分中的指令指向。 以下项目符号项讨论了 *monsamp* 中的某些 inf 编写器定义的部分：

-   **DEL \_当前 \_ 注册** 部分-标识要删除其值的四个注册表项： **模式**、 **MaxResolution**、 **DPMS** 和 **ICMProfile**。 后续部分中的新值会相应地更新这些密钥。

    ```inf
    [DEL_CURRENT_REG]
    HKR,MODES
    HKR,,MaxResolution
    HKR,,DPMS
    HKR,,ICMProfile
    ```

-   **1280** 部分--将 **MaxResolution** 注册表项更新为显示的字符串值。

    ```inf
    [1280]
    HKR,,MaxResolution,,"1280, 1024"
    ```

-   **DPMS** 节--将 **DPMS** 注册表项更新为 1 (TRUE) 。 对于不支持电源管理的监视器，以下行应将 **DPMS** 键值设置为 0 (FALSE) 。

    ```inf
    [DPMS]
    HKR,,DPMS,,1
    ```

-   [**AddReg**](../install/inf-addreg-directive.md) 部分-可以在监视器 INF 的 "外接程序" 部分中的 " **模式** " 键下指定项，以识别监视器支持的分辨率和计时。 如果 INF 以这种方式指定模式，则模式的条目将覆盖监视器的扩展显示信息数据 (*EDID*) 中指定的值。 因此，只有当 EDID 或 EDID 解释中存在问题时，才应使用 **模式** 密钥 INF 值。

    **模式** 键的每个子项指定一个分辨率，并且最多可以包含9个用于指定特定计时或计时范围的值。 每个子项名称的解析必须是两个整数值的组合：宽度和高度，用逗号分隔。 具体的时间从 **Mode1** 到 **Mode9**。 命名必须是连续的。 字符串值允许将水平和垂直同步脉冲的频率指定为单个值或范围，其中，范围指定为最小值，后跟一个短划线 (-) ，后跟最大值。 Frequency 值当前仅被解释为整数，该整数后面的任何数字都将被忽略。 字符串允许指定水平和垂直同步脉冲的极性。 但是，这些极性值当前被忽略。 每个字符串中只有最大水平同步脉冲值是必需的。 例如，下面显示了对于每个子字符串，方括号中的信息是可选的：

    ```inf
    [{MinHSync}-]{MaxHSync}[,{MinVSync}-{MaxVSynx}] 
    ```

    因此，可以在没有垂直同步范围的情况下指定每个子字符串。 但是，不建议指定没有垂直同步范围的子字符串。

    下面的第一行将 **"模式 \\ 1280，1024"** 子项设置为显示的字符串值。 同一行还标识了此子项的值名称 **Mode1**。 **Mode1** 子项后面的字符串中的第一对数字以 KHz 为水平指定了水平同步频率范围。 此字符串中的下一对数字指定垂直同步频率的范围，以 Hz 为赫兹。 在第二行中， **PreferredMode** 注册表项设置为伴随字符串中显示的值。 字符串中的值用于设置水平和垂直分辨率（以像素为单位）和屏幕刷新率（赫兹 (Hz) ，适用于首选屏幕模式）。 在 **PreferredMode** 字符串中，只需要水平和垂直解析值。 例如，以下内容显示，对于 **PreferredMode** 字符串，方括号中的信息是可选的：

    ```inf
    {Width},{Height}[,{Frequency}]
    ```

    因此，无需频率即可指定首选模式。 但是，不建议指定没有频率的首选模式。

    第三行将 **ICMProfile** 键设置为字符串值 **"profile1"**。

    ```inf
    [ACME-1234.AddReg]
    HKR,"MODES\1280,1024",Mode1,,"27.0-106.0,55.0-160.0,+,+"
    HKR,,PreferredMode,,"1024,768,70"
    HKR,,ICMProfile,0,"profile1.icm"
    ```

    对于满足 sRGB 规范的监视器（首选），无需监视器配置文件。
