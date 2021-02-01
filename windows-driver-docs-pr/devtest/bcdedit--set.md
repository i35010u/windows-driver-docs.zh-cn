---
title: BCDEdit /set
description: BCDEdit/set 命令在 Windows 的启动配置数据存储 (BCD) 中设置启动项目选项值。
ms.date: 01/25/2021
keywords:
- BCDEdit /set 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /set
api_type:
- NA
ms.localizationpriority: high
ms.custom: contperf-fy21q2
ms.openlocfilehash: 78cee4564790032466d6790c8d51fbd9c4358f15
ms.sourcegitcommit: 7b3bddc91b87de5afce36c120620497c37234fbf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98811994"
---
# <a name="bcdedit-set"></a>BCDEdit /set

BCDEdit/set 命令在 Windows 启动配置数据存储 (BCD) 中设置启动项目选项值。 使用 BCDEdit /set 命令可配置特定的启动项目元素，如内核调试程序设置、内存选项或启用测试签名的内核模式代码或负载备用硬件抽象层 (HAL) 的选项和内核文件。 若要删除启动项目选项，请使用 [BCDEdit/deletevalue](bcdedit--deletevalue.md) 命令。

> [!CAUTION]
> 需要管理权限才能使用 BCDEdit 来修改 BCD。 使用 BCDEdit /set 命令更改某些启动项目选项可能导致计算机无法运行。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="alternatives-to-bcdedit"></a>BCDEdit 的替代方案

### <a name="settings-startup-options"></a>设置启动选项

> [!TIP]
> 若要避免出现与使用 BCDEdit 相关的风险，请考虑使用本部分中所述的替代方法来执行启动配置。

### <a name="startup-settings"></a>“启动设置”

可在启动选项中使用一些常见的启动选项，例如启用调试模式。  在 Windows 10 中，可以在“设置”>“更新和安全”中选择“恢复”来访问该设置。 在“高级启动”下，选择“立即重新启动”。 计算机重新启动后，选择“启动”选项。 接下来，选择“排除故障”>“高级选项”>“启动设置”，然后选择“重新启动”按钮。 计算机重新启动后，你将能够设置可用的启动选项。

### <a name="system-configuration-utility"></a>系统配置实用工具

尽可能地使用系统配置实用工具 (MSConfig.exe) 而不是 BCDEdit。 有关详细信息，请参阅[如何在 Windows 10 中打开 MSConfig](https://support.microsoft.com/help/4026130/windows-how-to-open-msconfig-in-windows-10)。

## <a name="syntax"></a>语法

```syntax
bcdedit  /set [{ID}] datatype value
```

## <a name="parameters"></a>参数

\[ **{ID}** \]  
{ID} 是与启动项关联的 GUID。 如果未指定 {ID}，命令将修改当前操作系统启动项。 如果指定了启动目，则必须用大括号 { } 将与启动项关联的 GUID 括起来。 要查看所有活动启动项的 GUID 标识符，请使用 bcdedit /enum 命令。 当前启动项的标识符是 {current}。 有关此选项的详细信息，请使用以下命令：bcdedit /?ID

> [!NOTE]
> 如果使用 [Windows PowerShell](/powershell/module/Microsoft.PowerShell.Core/)，必须使用引号将启动项标识符引起来，例如：“{49916baf-0e08-11db-9af4-000bdbd316a0}”或“{current}” 。

*datatype* *value*  

## <a name="use-the-command-line-help-to-view-options"></a>使用命令行帮助查看选项

使用 BCDEdit 的命令行帮助显示可用于特定 Windows 版本的信息。

```console
C:\> BCDEdit /?

BCDEDIT - Boot Configuration Data Store Editor

The Bcdedit.exe command-line tool modifies the boot configuration data store.
The boot configuration data store contains boot configuration parameters and
controls how the operating system is booted. These parameters were previously
in the Boot.ini file (in BIOS-based operating systems) or in the nonvolatile
RAM entries (in Extensible Firmware Interface-based operating systems). You can
use Bcdedit.exe to add, delete, edit, and append entries in the boot
configuration data store.

For detailed command and option information, type bcdedit.exe /? <command>. For
example, to display detailed information about the /createstore command, type:

 bcdedit.exe /? /createstore

For an alphabetical list of topics in this help file, run "bcdedit /? TOPICS".
```

以下部分介绍了一些常见的数据类型及其相关值 。

## <a name="boot-settings"></a>启动设置

**bootlog** \[ **yes** | **no** \]  
启用系统初始化日志。 此日志存储在 %WINDIR% 目录中的 Ntbtlog.txt 文件中。 它包括以文本格式加载和卸载的驱动程序列表。

**bootmenupolicy** \[ **Legacy** | **Standard** \]  
定义系统将使用的启动菜单类型。 对于 Windows 10、Windows 8.1、Windows 8 和 Windows RT，默认值为 Standard。 对于 Windows Server 2012 R2 和 Windows Server 2012，默认值为 Legacy。 选择 Legacy 时，“高级选项”菜单 (F8) 可用 。 选择 Standard 时，仅在某些情况下会显示启动菜单：例如，出现启动故障、从修复磁盘或安装媒体启动、配置了多个启动项目或手动配置了计算机以使用高级启动。 选择 Standard 时，在启动过程中将忽略 F8 键 。 Windows 8 电脑会快速启动，因此没有足够的时间按 F8。 有关详细信息，请参阅[ Windows 启动设置（包括安全模式）](https://support.microsoft.com/help/17076/windows-8-startup-settings-safe-mode)。

> [!NOTE]
> 此选项从 Windows 8 和 Windows Server 2012 开始提供。 还可以使用 onetimeadvancedoptions 在下一次启动时使用一次高级选项 (F8) 菜单 (Legacy)  。

**bootstatuspolicy** *policy*

控制启动状态策略。 启动状态策略可以是以下项之一：

|启动状态策略 | 说明 |
|-------------------|-------------|
| **DisplayAllFailures**| 如果存在启动故障、关闭故障或检查点故障，则将显示所有错误。 重新启动时，计算机会将故障转移到 Windows 恢复环境。 |
|**IgnoreAllFailures**| 如果存在启动故障、关闭故障或检查点故障，则将忽略所有错误。 出现错误后，计算机将尝试正常启动。 |
|**IgnoreShutdownFailures**| 仅关机失败时，才忽略错误。 如果关机失败，计算机不会在重新启动时自动故障转移到 Windows 恢复环境。 这是 Windows 8 的默认设置。 |
|**IgnoreBootFailures**| 仅启动失败时，才忽略错误。 如果启动失败，计算机不会在重新启动时自动故障转移到 Windows 恢复环境。 |
|**IgnoreCheckpointFailures**| 仅检查点失败时，才忽略错误。 如果检查点失败，计算机不会在重新启动时自动故障转移到 Windows 恢复环境。 此选项从 Windows 8 和 Windows Server 2012 开始提供。 |
|**DisplayShutdownFailures**| 仅关机失败时，才显示错误。 如果关机失败，计算机会在重新启动时故障转移到 Windows 恢复环境。 忽略启动故障和检查点故障。 此选项从 Windows 8 和 Windows Server 2012 开始提供。 |
|**DisplayBootFailures**| 仅启动失败时，才显示错误。 如果启动失败，计算机会在重新启动时故障转移到 Windows 恢复环境。 忽略关机故障和检查点故障。 此选项从 Windows 8 和 Windows Server 2012 开始提供。 |
|**DisplayCheckpointFailures**| 仅检查点失败时，才显示错误。 如果检查点失败，计算机会在重新启动时故障转移到 Windows 恢复环境。 忽略启动和关机故障。 此选项从 Windows 8 和 Windows Server 2012 开始提供。 |

**quietboot** \[ **on** | **off** \]  
控制高分辨率位图的显示，以代替 Windows 启动屏幕的显示和动画。

> [!NOTE]
> 请勿在 Windows 8 中使用 quietboot 选项，因为它会阻止显示错误检查数据（所有启动图形除外）。

**sos** \[ **on** | **off** \]  
控制驱动程序在启动过程中加载时的名称的显示。 使用 sos on 可显示名称。 使用 sos off 可禁止显示。

**lastknowngood** \[ **on** | **off** \]  
使能够启动到最后一次的正确配置。

**nocrashautoreboot** \[ **on** | **off** \]  
在崩溃时禁用自动重启。

**resumeobject (id)**  
定义与此操作系统对象相关的恢复对象的标识符。

**safebootalternateshell** \[ **on** | **off** \]  
启动进入安全模式时，使用可选的 shell。

**winpe** \[ **on** | **off** \]  
使计算机能够启动到 Windows PE。

**onetimeadvancedoptions** \[ **on** | **off** \]  
控制系统是否引导到下一个启动时的旧菜单（F8 菜单）。

```syntax
bcdedit /set {current} onetimeadvancedoptions on
```

## <a name="display-settings"></a>显示设置

**bootuxdisabled** \[ **on** | **off** \]  
禁用启动图形。

**graphicsmodedisabled** \[ **on** | **off** \]    
指示是否已禁用图形模式且启动应用程序是否必须使用文本模式显示。

**graphicsresolution**  
定义图形分辨率：1024x768、800x600 和 1024x600 等。

**highestmode** \[ **on** | **off** \]  
使启动应用程序能够使用固件公开的最高级别的图形模式。

**novga** \[ **on** | **off** \]  
完全禁止使用 VGA 模式。

**vga** \[ **on** | **off** \]  
强制使用 VGA 显示驱动程序。

## <a name="hardware-abstraction-layer-hal--kernel"></a>硬件抽象层 (HAL) 和 KERNEL

**hal** *file*  
引导操作系统加载程序来加载备用 HAL 文件。 指定的文件必须位于 %SystemRoot%\\system32 目录中。

**kernel** *file*  
引导操作系统加载程序来加载备用内核。 指定的文件必须位于 %SystemRoot%\\system32 目录中。

## <a name="verification-settings"></a>验证设置

**testsigning** \[ **on** | **off** \]  
控制 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 或 Windows Vista 是否会加载任何类型的测试签名内核模式代码。 默认情况下不设置此选项，这意味着在 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 和 Windows Vista 的 64 位版本上默认不加载测试签名的内核模式驱动程序。 运行 BCDEdit 命令后，重启计算机，使更改生效。 有关详细信息，请参阅 [测试签名简介](../install/introduction-to-test-signing.md)

**nointegritychecks** \[ **on** | **off** \] 禁用完整性检查。 启用安全启动时无法设置。 Windows 7 和 Windows 8 将忽略此值。

**disableelamdrivers** \[ **yes** | **no** \]  
控制开机初期启动的反恶意软件 (ELAM) 驱动程序的加载。 出于安全原因，OS 加载程序删除了此条目。 此选项只能通过使用 F8 菜单触发。 用户必须当场出现（在计算机上）才能触发此选项。

> [!NOTE]
> 此选项应仅用于调试。

**nx** \[**Optin \|OptOut \| AlwaysOn \|AlwaysOff**\]  
启用、禁用和配置数据执行保护 (DEP)，这是一组硬件和软件技术，旨在防止有害代码在受保护的内存位置运行。 有关 DEP 设置的信息，请参阅[数据执行保护](/windows/desktop/Memory/data-execution-prevention)。

|DEP 选项 | 说明 |
|-----------|-------------|
|**Optin**| 仅为操作系统组件启用 DEP，包括 Windows 内核和驱动程序。 管理员可以使用应用程序兼容性工具包 (ACT) 在选定的可执行文件上启用 DEP。 |
|**Optout** | 为操作系统和所有进程（包括 Windows 内核和驱动程序）启用 DEP。 但是，管理员可以使用“控制面板”中的“系统”来禁用所选可执行文件的 DEP 。 |
|**AlwaysOn** | 为操作系统和所有进程（包括 Windows 内核和驱动程序）启用 DEP。 将忽略禁用 DEP 的所有尝试。 |
|**AlwaysOff** | 禁用 DEP。 将忽略有选择地启用 DEP 的尝试。 在 Windows Vista 上，还可使用此参数禁用物理地址扩展 (PAE)。 在 Windows Server 2008 上，使用此参数无法禁用 PAE。 |

## <a name="processor-settings"></a>处理器设置

**groupsize** *maxsize*  
设置单个处理器组中逻辑处理器的最大数量，其中最大大小为介于 1 到 64（含）之间 2 的任意次幂。 默认情况下，处理器组的最大大小为 64 个逻辑处理器。 可以使用此启动配置设置来替代计算机处理器组的大小和组成，以便进行测试。 [处理器组](/windows/win32/procthread/processor-groups)对具有超过 64 个逻辑处理器的计算机提供支持。 此启动选项适用于 64 位版本的 Windows 7 和 Windows Server 2008 R2 及更高版本。 此启动选项对 32 位版本的 Windows 7 不起作用。

如果要强制多个组，并且计算机的可用逻辑处理器不超过 64 个，请使用 groupsize 选项。 有关使用此选项的详细信息，请参阅[用于测试驱动程序是否支持多个处理器组的启动参数](./boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

**groupaware** \[ **on** | **off** \]  
强制驱动程序了解多个处理器组环境中的多个组。 使用此选项可帮助公开驱动程序和组件中的跨组不兼容性。 [处理器组](/windows/win32/procthread/processor-groups)对具有超过 64 个逻辑处理器的计算机提供支持。 此启动选项适用于 64 位版本的 Windows 7 和 Windows Server 2008 R2 及更高版本。 此启动选项对 32 位版本的 Windows 7 不起作用。 当计算机的可用逻辑处理器不超过 64 个时，可以使用 groupaware 选项和 groupsize 选项来测试驱动程序是否与多个组兼容 。

groupaware on 设置可确保进程在组 0 以外的组中启动。 这增加了驱动程序和组件之间跨组交互的机会。 该选项还会修改旧函数 KeSetTargetProcessorDpc、KeSetSystemAffinityThreadEx 和 KeRevertToUserAffinityThreadEx 的行为，以便它们始终对包含可用逻辑处理器的最高编号组进行操作  。 调用任何这些旧函数的驱动程序应更改为调用其组感知对应项（KeSetTargetProcessorDpcEx、KeSetSystemGroupAffinityThread 和 KeRevertToUserGroupAffinityThread）  。

有关使用此选项的详细信息，请参阅[用于测试驱动程序是否支持多个处理器组的启动参数](./boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

**maxgroup** \[ **on** | **off** \]  
最大化在处理器组配置中创建的组数。 “maxgroup on”设置以最大化特定计算机的组数的方式将 NUMA 节点分配给组。 创建的组数是计算机具有的 NUMA 节点数，或者此 Windows 版本支持的最大组数（以较小者为准）。 默认行为 (maxgroup off) 是将 NUMA 节点紧密地打包到尽可能少的组中。

如果想要使用多个组，计算机的可用逻辑处理器不超过 64 个，并且计算机已具有多个 NUMA 节点，则请使用 maxgroup 选项。 如果计算机的逻辑处理器数超过 64 个，那么还可使用此选项来更改计算机的默认组配置。

[处理器组](/windows/desktop/ProcThread/processor-groups)对具有超过 64 个逻辑处理器的计算机提供支持。 此选项适用于 64 位版本的 Windows 7 和 Windows Server 2008 R2 及更高版本。 此启动选项对 32 位版本的 Windows 7 不起作用。

有关使用此选项的详细信息，请参阅[用于测试驱动程序是否支持多个处理器组的启动参数](boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

**onecpu** \[ **on** | **off** \]  
仅强制在具有多个逻辑处理器的计算机中使用启动 CPU 。 例如，以下命令将当前操作系统加载程序配置为使用一个处理器。

```syntax
bcdedit /set onecpu on
```

## <a name="memory-related-settings"></a>与内存相关的设置

**increaseuserva** *Megabytes*  
指定用户模式虚拟地址空间的内存量 (MB)。

在 Windows 的 32 位版本中，应用程序的可用虚拟地址空间为 4 GB。 分配此虚拟地址空间，让应用程序使用 2 GB 空间，另外 2 GB 仅限系统使用。

使用 increaseuserva 选项启用的 4 GB 调优功能，可以将应用程序可用的虚拟地址空间增加到 3 GB，从而将系统可用的内存量减少到 1 到 2 GB。 BCEdit /set increaseuserva Megabytes 命令可以指定十进制表示法中 2048 (2 GB) 和 3072 (3 GB) 兆字节之间的任何值。 Windows 使用剩余的地址空间（4 GB 减去指定数量）作为其内核模式地址空间。

有关此功能的其他信息，请参阅 [4 GB 优化 (Windows)](/windows/desktop/Memory/4-gigabyte-tuning)。

**nolowmem** \[ **on** | **off** \] 控制低内存的使用。 指定为“nolowmem on”时，此选项会将操作系统、设备驱动程序和所有应用程序加载到 4 GB 边界以上的地址中，并指示 Windows 在 4 GB 边界以上的地址分配所有内存池。 请注意，Windows 8、Windows Server 2012 和 Windows 更高版本会忽略 nolowmem 选项。

**pae** \[ **Default** | **ForceEnable** | **ForceDisable** \]  
启用或禁用物理地址扩展 (PAE)。 启用 PAE 后，系统将加载 Windows 内核的 PAE 版本。

pae 参数仅在 32 位版本的 Windows 的启动项目上有效，该版本在具有基于 x86 和 x64 的处理器的计算机上运行。 在 Windows 的 32 位版本（Windows 8 之前）上，默认情况下禁用 PAE。 但是，计算机配置为内存范围超过 4 GB 区域的热添加内存设备时，Windows 会自动启用 PAE，这是静态资源关联表 (SRAT) 定义的。 “热添加内存”支持无需重新启动或关闭计算机即可添加的内存设备。 在这种情况下，由于必须在系统启动时启用 PAE，因此会自动启用它，以便系统可以立即对重启之间添加的扩展内存进行寻址。 热添加内存仅在以下版本中受支持：Windows Server 2008（数据中心版本）、面向基于 Itanium 系统的 Windows Server 2008 以及所有更高版本的 Windows Server 的数据中心和企业版。 此外，对于 Windows Server 2008 之前的 Windows 版本，热添加内存仅在具有 ACPI BIOS、x86 处理器和专用硬件的计算机上受支持。 对于 Windows Server 2008 和更高版本的 Windows Server，所有处理器体系结构都支持热添加内存。

对于支持启用硬件的数据执行保护 (DEP) 的计算机，如何正在运行支持 DEP 的 32 位版本的 Windows 操作系统，则启用 DEP 时会在所有 32 位版本的 Windows 操作中（Windows Server 2003 SP1 除外）自动启用 PAE，并在禁用 DEP 时禁用 PAE。 若要在禁用 DEP 时启用 PAE，必须通过使用 /set nx AlwaysOff 和 /set pae ForceEnable 来显式启用 PAE 。 有关 DEP 的详细信息，请参阅[用于配置 DEP 和 PAE 的启动参数](./boot-parameters-to-configure-dep-and-pae.md)。

有关使用 pae 参数和影响 PAE 配置的其他参数的详细信息，请参阅[用于配置 DEP 和 PAE 的启动参数](./boot-parameters-to-configure-dep-and-pae.md)。

**removememory** *Megabytes*  
从操作系统可使用的总可用内存中删除内存。

例如，以下命令从与指定启动项关联的操作系统可用的总计中删除 256 MB 的内存。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} removememory 256
```

**truncatememory** *address* 限制 Windows 可用的物理内存量。 使用此选项时，Windows 会忽略指定物理地址或以上的所有内存。 指定地址（以字节为单位）。

例如，以下命令将物理地址限制设置为 1 GB。 可以以十进制 (1073741824) 或十六进制 (0x40000000) 指定地址。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} truncatememory 0x40000000
```

## <a name="additional-settings"></a>其他设置

**disabledynamictick** \[ **yes** | **no** \]  
启用和禁用动态计时器时钟周期功能。

> [!NOTE]
> 此选项应仅用于调试。

**forcelegacyplatform** \[ **yes** | **no** \]  
强制 OS 假定存在旧式电脑设备，如 CMOS 和键盘控制器。

> [!NOTE]
> 此选项应仅用于调试。

**pciexpress** \[ **default** | **forcedisable**\]  
启用或禁用 PCI Express 功能。 如果计算机平台支持 PCI Express 功能，并且 ACPI \_OSC 方法将功能的控制权授予操作系统，Windows 将通过 PCI Express 本机控制功能启用高级功能（这是默认设置）。 使用 forcedisable 选项替代高级 PCI Express 功能并使用旧版 PCI Express 行为。 有关详细信息，请参阅[在 Windows 中启用 PCI Express 本机控制](/previous-versions/windows/hardware/design/dn631753(v=vs.85))。

**tpmbootentropy** \[ **default** | **ForceEnable** | **ForceDisable**\]  
确定是否从受信任的平台模块 (TPM) 收集熵，以帮助在操作系统中设定随机数生成器的种子。

**tscsyncpolicy** \[ **Default** | **Legacy** | **Enhanced** \]  
控制时间戳计数器同步策略。 此选项应仅用于调试。

**usefirmwarepcisettings** \[ **yes** | **no** \]  
启用或禁用使用 BIOS 配置的外围组件互连 (PCI) 资源。

**useplatformclock** \[ **yes** | **no** \]  
强制使用平台时钟作为系统的性能计数器。

> [!NOTE]
> 此选项应仅用于调试。

**uselegacyapicmode** \[ **yes** | **no** \]  
用于强制旧的 APIC 模式，即使处理器和芯片集支持扩展 APIC 模式也是如此。

**useplatformtick** \[ **yes** | **no** \]  
强制时钟由平台源备份，不允许合成计时器。 该选项从 Windows 8 和 Windows Server 2012 开始提供。

> [!NOTE]
> 此选项应仅用于调试。

**xsavedisable** \[ **0** | **1** \]  
设置为零 (0) 以外的值时，禁用内核中的 XSAVE 处理器功能。

**x2apicpolicy** \[ **enable** | **disable** \]  
启用或禁用扩展 APIC 模式（如果支持）。 如果系统可用，则默认使用扩展的 APIC 模式。

## <a name="debugger-settings"></a>调试程序设置

若要使用调试程序设置，请使用以下命令。

|Command|说明|
|-------|-----------|
[BCDEdit /bootdebug](bcdedit--bootdebug.md)|/bootdebug 启动选项可启用或禁用当前或指定的 Windows 操作系统启动项目的启动调试。|
|[BCDEdit /dbgsettings](bcdedit--dbgsettings.md)|/dbgsettings 选项可设置或显示计算机的当前全局调试程序设置。 若要启用或禁用内核调试程序，请使用 BCDEdit /debug 选项。|
|[BCDEdit /debug](bcdedit--debug.md)|/debug 启动选项可启用或禁用与指定的启动项目或当前启动项目关联的 Windows 操作系统的内核调试。|

## <a name="hypervisor-debugger-settings"></a>虚拟机监控程序调试程序设置

使用 BCDEdit / hypervisorsettings 选项来设置或显示系统的调试程序设置调试程序设置。 有关详细信息，请参阅 [BCDEdit /hypervisorsettings](bcdedit--hypervisorsettings.md)。

**hypervisordebug** \[ **On** | **Off** \]  
控制是否启用虚拟机监控程序调试器。

## <a name="hypervisor-settings"></a>虚拟机监控程序设置

**hypervisoriommupolicy** \[ **default** | **enable** | **disable**\]  
控制虚拟机监控程序是否使用输入输出内存管理单元 (IOMMU)。

**hypervisorlaunchtype** \[ **Off** | **Auto** \]  
控制虚拟机监控程序启动选项。 如果要设置调试器以在目标计算机上调试 Hyper-V，请在目标计算机上将此选项设置为“自动”。 有关详细信息，请参阅[使用 Hyper-V 创建虚拟机](/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**hypervisorloadoptions NOFORCESNOOP** \[ **Yes** | **No** \]  
指定虚拟机监控程序是否应对系统 IOMMU 执行窥探控制。

**hypervisornumproc** *number*  
指定可在虚拟机监控程序中启动的逻辑处理器的总数。

**hypervisorrootproc** *number*  
指定根分区中虚拟处理器的最大数量，并限制拆分后非一致性内存体系结构 (NUMA) 节点的数量，这些节点可以在虚拟机监控程序中启动逻辑处理器。

**hypervisorrootprocpernode** *number*  
指定根分区中可在预拆分非一致性内存体系结构 (NUMA) 节点内启动的虚拟处理器总数。

**hypervisoruselargevtlb** \[ **yes** | **no**\]  
增加虚拟 Translation Lookaside Buffer (TLB) 大小。

## <a name="emergency-management-services"></a>紧急管理服务

BCDEdit /ems 选项可启用或禁用指定的操作系统启动项目的紧急管理服务 (EMS)。 有关详细信息，请参阅 [BCDEdit /ems](bcdedit--ems.md)。

BCDEdit /emssettings 选项可设置计算机的全局紧急管理服务 (EMS) 设置。 有关详细信息，请参阅 [BCDEdit /emssettings](bcdedit--emssettings.md)。

## <a name="event-logging"></a>事件日志记录

BCDEdit /event 命令可启用或禁用指定启动项目的远程事件日志记录。 有关详细信息，请参阅 [BCDEdit /event](bcdedit--event.md)。

### <a name="comments"></a>备注

有关特定 BCD 元素和启动选项的详细信息，可以使用命令 BCDEdit /?OSLOADER 和 BCDEdit /?TYPES OSLOADER。

若要查看当前启动项及其设置，请使用 bcdedit /enum 命令。 此命令显示可用启动项及其关联的全局唯一标识符 (GUID)。 使用带有 /set 命令的标识符来配置特定启动项的选项。

若要删除已设置的启动选项值，请使用 /deletevalue 选项。 该命令的语法如下：

**bcdedit** /**deletevalue** \[ **{ID}** \] *datatatype*

例如，如果将处理器组选项 groupsize 更改为用于测试目的的新值，则可以通过键入以下命令，然后重启计算机，恢复到默认值 64。

``` syntax
bcdedit /deletevalue groupsize
```

对启动选项的任何更改都需要重启才能生效。 有关常用 BCDEdit 命令的详细信息，请参阅[引导配置数据编辑器常见问题](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc721886(v=ws.10))。

## <a name="dtrace"></a>DTrace

DTrace (DTrace.exe) 是一个命令行工具，用于显示系统信息和事件。 其中有一个用于启用 dtrace 的 bcedit 选项。 有关可用的 DTrace BCDEdit 选项的信息，请参阅 [Windows 上的 DTrace](/windows-hardware/drivers/devtest/dtrace) 的“安装”部分。

## <a name="requirements"></a>要求

**支持的最低客户端版本**：Windows Vista

**支持的最低服务器版本**：Windows Server 2008

## <a name="see-also"></a>另请参阅

- [BCDEdit 选项参考](bcd-boot-options-reference.md)
- [BCDEdit /deletevalue](bcdedit--deletevalue.md)
