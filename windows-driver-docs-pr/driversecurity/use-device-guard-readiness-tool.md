---
title: 使用 Device Guard 准备工具来评估 HVCI 驱动程序兼容性
description: 请按照下列步骤以使用设备防护准备工具来评估 HVCI 驱动程序兼容性的驱动程序代码。
ms.assetid: ''
ms.date: 02/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4a31a354f05f96623fc1bfc30e32e9f9c4f203
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58845550"
---
# <a name="use-the-device-guard-readiness-tool-to-evaluate-hvci-driver-compatibility"></a>使用 Device Guard 准备工具来评估 HVCI 驱动程序兼容性

## <a name="overview"></a>概述

设备防护准备工具用于检查数创建支持不同的安全增强功能的 PC 的要求。 本部分介绍如何使用该工具来评估驱动程序的受保护的虚拟机监控程序代码完整性 (HVCI) 环境中运行的能力。 

测试 HVCI 驱动程序 Device Guard 兼容性的 OS 和硬件要求：

1. Windows:在所有版本的 Windows，如 Windows Pro、 Windows 10 企业版、 Windows Server 和 Windows 10 IoT 企业版 （不支持在 S 模式下） 上可用。

2. 硬件：支持 SLAT 的虚拟化扩展插件的最新硬件。

若要准备工具用于评估的其他要求，如安全启动，请参阅下载的准备情况工具中包含的 readme.txt 文件。

有关相关的设备基础测试的详细信息，请参阅[Device.DevFund 测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-tests)。

## <a name="implement-device-guard-compatible-code"></a>实现 Device Guard 兼容代码

若要实现 Device Guard 兼容代码，请确保您的驱动程序代码将执行以下操作：

- 选择启用 NX 默认情况下
- 有关内存分配 (NonPagedPoolNx) 使用 NX Api/标志
- 不使用是可写和可执行文件的部分
- 不会尝试直接修改可执行文件系统内存
- 不在内核中使用动态代码
- 不会加载为可执行文件的数据文件
- 节对齐是倍数 0x1000 (页\_大小)。 例如 驱动程序\_对齐方式 = 0x1000

不保留供系统使用的 DDIs 以下列表可能会受到影响：

|                                                                                                      |
|------------------------------------------------------------------------------------------------------|
| DDI 名称                                                                                             |
| [**ExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff544501)                                                          |
| [**ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)                                        |
| [**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)                                  |
| [**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)                                            |
| [**ExAllocatePoolWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff544523)                            |
| [**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)                        |
| [**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)                                |
| [**MmAllocateContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554460)                                  |
| [**MmAllocateContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554464)          |
| [**MmAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff554469)  |
| [**MmAllocateContiguousNodeMemory**](https://msdn.microsoft.com/library/windows/hardware/jj602795)                          |
| [**MmCopyMemory**](https://msdn.microsoft.com/library/windows/hardware/dn342884)                                                              |
| [**MmMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff554618)                                                              |
| [**MmMapLockedPages**](https://msdn.microsoft.com/library/windows/hardware/ff554622)                                                      |
| [**MmMapLockedPagesSpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff554629)                              |
| [**MmProtectMdlSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554670)                                    |
| [**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)                                        |
| [**ZwCreateSection**](https://msdn.microsoft.com/library/windows/hardware/ff566428)                                                        |
| [**ZwMapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff566481)                                                  |
| [**NtCreateSection**](https://msdn.microsoft.com/library/windows/hardware/ff556473)                                                        |
| [**NtMapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff556551)                                                  |
| [**ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)                                    |
| NDIS                                                                                                 |
| [**NdisAllocateMemoryWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff561606)                  |
| 存储                                                                                              |
| [**StorPortGetDataInBufferSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/jj553720)             |
| [**StorPortGetSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff567100)                                     |
| [**ChangerClassAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff551402)                                     |
| 显示                                                                                              |
| [*DxgkCbMapMemory*](https://msdn.microsoft.com/library/windows/hardware/ff559533)                                                         |
| [**VideoPortAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff570180)                                           |
| 音频微型端口                                                                                       |
| [**IMiniportDMus::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536701)                                        |
| [**IMiniportMidi::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536710)                                        |
| [**IMiniportWaveCyclic::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536723)                            |
| [**IPortWavePci::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536916)                      |
| [**IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)                                  |
| 音频端口类                                                                                     |
| [**PcNewDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff537712)                                                         |
| [**PcNewResourceList**](https://msdn.microsoft.com/library/windows/hardware/ff537717)                                                     |
| [**PcNewResourceSublist**](https://msdn.microsoft.com/library/windows/hardware/ff537718)                                               |
| IFS                                                                                                  |
| [**FltAllocatePoolAlignedWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff541762)                              |
| [**FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)                                                    |
| WDF                                                                                                  |
| [**WdfLookasideListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548694)                                             |
| [**WdfMemoryCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548706)                                                           |
| [**WdfDeviceAllocAndQueryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff545882)                             |
| [**WdfDeviceAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265599)                         |
| [**WdfFdoInitAllocAndQueryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff547239)                           |
| [**WdfFdoInitAllocAndQueryPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/dn265612)                       |
| [**WdfIoTargetAllocAndQueryTargetProperty**](https://msdn.microsoft.com/library/windows/hardware/ff548585)             |
| [**WdfRegistryQueryMemory**](https://msdn.microsoft.com/library/windows/hardware/ff549920)                                             |


## <a name="using-the-dgr-tool"></a>使用 DGR 工具

若要使用设备防护准备工具，请完成以下步骤：

-   **准备测试 PC**

    *启用基于虚拟化的代码完整性保护*-运行系统信息应用程序 (msinfo32)。 查找以下项："Device Guard 虚拟化基于安全"。 它应显示："Running"。

    或者，此外还有一个 WMI 界面，用于检查使用的管理工具，可用于在 PowerShell 中显示的信息。

    ```console
    Get-CimInstance –ClassName Win32_DeviceGuard –Namespace root\Microsoft\Windows\DeviceGuard
    ```

    有关如何中断输出显示的信息，请参阅[启用基于虚拟化的代码完整性保护](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/enable-virtualization-based-protection-of-code-integrity)。

    *禁用 Device Guard* -请注意，在运行时准备工具，Device Guard 必须禁用测试 PC 上如 Device Guard 可能会阻止加载后，该驱动程序和驱动程序不会将可用于准备工具来测试。

    *选择性地启用测试签名*-若要允许安装未签名的开发驱动程序，你可能想要启用测试签名使用 BCDEdit。

    ```console
    bcdedit /set TESTSIGNING ON 
    ```

-   **安装测试驱动程序**

    在目标测试 PC 上安装所需的测试驱动程序。

    **重要**已测试开发驱动程序并处理完所有代码问题后，重新测试最终的生产环境驱动程序。 此外，使用 HLK 测试驱动程序。 有关详细信息，请参阅[虚拟机监控程序代码完整性准备情况测试](https://msdn.microsoft.com/library/windows/hardware/dn955152)。



-   **安装设备防护准备工具**

    **警告**  
    设备防护准备工具更改注册表值，并且可能会影响安全启动等功能，如使用测试不包含任何数据或应用程序的 PC。 在运行测试后，你可能想要重新安装 Windows，才能重新建立所需的安全配置。

    1. 从此处下载该工具：[Device Guard 和 Credential Guard 硬件准备情况工具](https://www.microsoft.com/download/details.aspx?id=53337)。

    2. 解压缩该工具在目标测试计算机上。

-   **配置 PowerShell 以允许执行未签名的脚本。**

    准备工具是一个 PowerShell 脚本。 若要使用准备工具脚本，请打开管理员 PowerShell 脚本。

    如果执行策略不已设置为允许运行脚本，则应手动设置它，如下所示。

    ```powershell
    Set-ExecutionPolicy Unrestricted
    ```

-   **运行准备工具来启用 HVCI**

    1. 在 Powershell 中，找到在其中解压缩准备工具的目录。

    2. 运行准备工具以启用 HVCI。

    ```powershell
    DG_Readiness_Tool.ps1 -Enable HVCI
    ```

    3. 当定向，重启计算机。

-   **运行脚本，以评估 HVCI 功能**

    1. 运行准备工具来评估的驱动程序支持 HVCI 的功能。

    ```powershell
    DG_Readiness_Tool.ps1 -Capable HVCI
    ```

-   **计算输出**

    向屏幕输出是颜色编码。

    |                   |                                                                                                   |
    |-------------------|---------------------------------------------------------------------------------------------------|
    | 红色-错误      | 元素是缺少或未配置，将阻止启用和使用 DG/CG。                |
    | 黄色的警告 | 此设备可用于启用和使用 DG/CG，但其他安全优势将不会出现。 |
    | 绿色-消息  | 此设备已完全符合 DG/CG 要求。                                           |

    除了输出到屏幕上，默认情况下，具有详细的输出的日志文件位于 c:\\DGLogs

    有五个步骤 （或部分） 的设备防护准备工具输出中。 步骤 1 包含驱动程序兼容性信息。

    ```text
     ====================== Step 1 Driver Compat ====================== 
    ```

    显示为绿色的驱动程序必须标识的 HVCI 兼容性问题。 如果您有兴趣评估特定的驱动程序，如果驱动程序名称显示为绿色，并且处于活动状态且已加载，它已经通过 HVCI 兼容性测试。

    找到如下所示，在日志末尾的"不兼容的 HVCI 内核驱动程序模块"部分。

    ```text
    InCompatible HVCI Kernel Driver Modules found

    Module: TestDriver1.sys
        Reason: section alignment failures:             9
    Module: TestDriver2.sys
        Reason: execute pool type count:                3
    ```

    在上面所示示例中，两个驱动程序标识为不兼容。 TestDriver1.sys 出现内存部分对齐故障和 TestDriver2.sys 已配置为使用可执行文件的内存区域的池。

    设备驱动程序不兼容性的七种类型的统计信息是还可以使用 ！ verifier 调试器扩展。 有关详细信息 ！ verifier 扩展，请参阅[ **！ verifier**](https://msdn.microsoft.com/library/windows/hardware/ff565591)。

    ```text
            Execute Pool Type Count:                3
            Execute Page Protection Count:          0
            Execute Page Mapping Count:             0
            Execute-Write Section Count:            0
            Section Alignment Failures:             0
            Unsupported Relocs Count:               0
            IAT in Executable Section Count:        0
    ```



使用下表解释输出，并确定所需驱动程序代码更改以修复不同类型的 HVCI 不兼容问题。



<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>

<tr class="odd">
<td align="left"><strong>警告</strong></td>
<td align="left"><strong>兑换</strong></td>
</tr>

<tr class="even">
<td align="left"><p>Execute Pool Type（执行池类型）</p></td>
<td align="left"><p>调用者指定了可执行池类型。 调用请求可执行内存的内存分配函数。</p>
<p>确保所有池类型都包含不可执行的 NX 标志。</p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>Execute Page Protection（执行页保护）</p></td>
<td align="left"><p>调用者指定了可执行页面保护。</p>
<p>指定"无执行"页面保护掩码。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>Execute Page Mapping（执行页映射）</p></td>
<td align="left"><p>调用者指定了可执行的内存描述符列表 (MDL) 映射。</p>
<p> 确保使用的掩码包含 MdlMappingNoExecute。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff554559.aspx" data-raw-source="[MmGetSystemAddressForMdlSafe](https://msdn.microsoft.com/library/windows/hardware/ff554559.aspx)">MmGetSystemAddressForMdlSafe</a></p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>Execute-Write Section（执行-写入部分）</p></td>
<td align="left"><p>该图像包含可执行和可写部分。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>Section Alignment Failures（节对齐方式失败）</p>
</td>
<td align="left"><p>图像包含不是页面对齐的部分。</p>
<p>Section Alignment 必须是 0x1000（PAGE_SIZE）的倍数。 例如 DRIVER_ALIGNMENT=0x1000</p></td>
</tr>


<tr class="even">
<td align="left"><p>IAT 在可执行部分</p></td>
<td align="left"><p>导入地址表 (IAT) 不应该是内存的可执行部分。</p>
<p>当 IAT 位于内存中仅允许读取和执行 (RX) 的部分时，会发生此问题。 这意味着操作系统将无法写入 IAT 来为引用的 DLL 设置正确的地址。 </p>
<p> 发生这种情况的一种方法是使用时<a href="https://docs.microsoft.com/cpp/build/reference/merge-combine-sections" data-raw-source="[/MERGE (Combine Sections)](https://docs.microsoft.com/cpp/build/reference/merge-combine-sections)">/MERGE （合并节）</a>代码链接中的选项。 例如如果.rdata （只读的已初始化的数据） 合并与.text 的数据 （可执行代码），则可以在可执行部分中的内存可能最终会 IAT。  </p>
</td>
</tr>

</tbody>
</table>


---------

不支持重定位

<p>在 Windows 10 版本 1507年到 Windows 10 版本 1607 中，由于使用地址空间布局随机化 (ASLR) 出现问题的地址的对齐方式和内存重定位可能出现。  操作系统需要将地址从链接器设置的默认基址位置重定位到 ASLR 分配的实际位置。 此重定位不能跨越页面边界。  例如，考虑从某个页面上偏移量为 0x3FFC 的位置处开始的 64 位地址值。 其地址值重叠到了下一页上偏移量为 0x0003 的位置。 在 Windows 10，版本 1703年之前不支持这种重叠重定位。</p>

<p>当全局结构类型变量初始值设定项具有指向另一个全局变量的未对齐指针（其布局方式使链接器无法移动变量以避免跨越重定位）时，可能会发生这种情况。 链接器将尝试移动的变量，但在有些情况下，它可能无法执行此操作 （例如使用大型未对齐的结构或未对齐结构的大型数组）。 在适当的情况下，应使用 <a href="https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking" data-raw-source="[/Gy (COMDAT)](https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking)">/ Gy（COMDAT)</a> 选项组装模块以允许链接器尽可能地对齐模块代码。</p>



```cpp
#include <pshpack1.h>

typedef struct _BAD_STRUCT {
      USHORT Value;
      CONST CHAR *String;
} BAD_STRUCT, * PBAD_STRUCT;

#include <poppack.h>

#define BAD_INITIALIZER0 { 0, "BAD_STRING" },
#define BAD_INITIALIZER1 \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      \
      BAD_INITIALIZER0      

#define BAD_INITIALIZER2 \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      \
      BAD_INITIALIZER1      

#define BAD_INITIALIZER3 \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      \
      BAD_INITIALIZER2      

#define BAD_INITIALIZER4 \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      \
      BAD_INITIALIZER3      

BAD_STRUCT MayHaveStraddleRelocations[4096] = { // as a global variable
      BAD_INITIALIZER4
};
```

还有其他涉及使用汇编程序代码的情况，也可能发生此问题。

---------


## <a name="script-customization"></a>脚本自定义项

下面是 Regkeys Device Guard 和 Credential Guard 无 UEFI 锁到脚本的自定义项及其值的列表。

若要 HVCI 和 CG 无 UEFI 锁启用：

```reg
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "EnableVirtualizationBasedSecurity" /t REG_DWORD /d 1 /f' 
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "RequirePlatformSecurityFeatures" /t REG_DWORD /d 1 /f' 
```

## <a name="driver-verifier-code-integrity"></a>驱动程序验证程序代码完整性

使用该驱动程序验证程序代码完整性选项标志 (0x02000000) 以启用额外检查，验证符合此功能。 若要从命令行启用此功能，使用以下命令。

```console
verifier.exe /flags 0x02000000 /driver <driver.sys>
```
若要选择此选项，如果使用的验证程序 GUI，请选择*创建自定义设置*（适用于代码开发人员），选择*下一步*，然后选择_的代码完整性检查_。

验证程序命令行 /query 选项可用于显示当前驱动程序验证程序的信息。

```console
verifier /query 
```







