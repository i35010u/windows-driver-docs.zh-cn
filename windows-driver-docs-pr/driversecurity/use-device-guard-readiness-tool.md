---
title: 评估要求 HVCI 驱动程序兼容性
description: 请按照以下步骤来评估驱动程序代码的要求 HVCI 驱动程序兼容性。
ms.assetid: ''
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6e1f4331474b7dc9093483ee762e3059f13cce60
ms.sourcegitcommit: 969a98d4866be74e145df617a9f0963053898a0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153163"
---
# <a name="evaluate-hvci-driver-compatibility"></a>评估要求 HVCI 驱动程序兼容性

## <a name="overview"></a>概述

DGReadiness 工具旨在检查多种需求，用于创建支持各种安全增强功能的 PC。 本部分介绍如何使用该工具评估驱动程序在受管理程序保护的代码完整性（要求 HVCI）环境中运行的能力。

用于测试要求 HVCI 驱动程序兼容性的操作系统和硬件要求：

1. Windows：适用于所有版本的 Windows，例如 Windows Pro、Windows 10 企业版、Windows Server 和 Windows 10 IoT Enterprise （在 S 模式下不受支持）。

2. 硬件：最新硬件，支持使用 SLAT 的虚拟化扩展。

若要使用准备工具来评估其他要求，例如安全启动，请参阅准备工具下载中包含的 readme.txt 文件。

有关相关设备基础测试的详细信息，请参阅[DevFund 测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-tests)。

## <a name="implement-hvci-compatible-code"></a>实现与要求 HVCI 兼容的代码

若要实现要求 HVCI 兼容的代码，请确保你的驱动程序代码执行以下操作：

- 默认情况下，使用 NX
- 使用 NX Api/标志进行内存分配（NonPagedPoolNx）
- 不使用可写和可执行的节
- 不尝试直接修改可执行系统内存
- 不使用内核中的动态代码
- 不将数据文件加载为可执行文件
- 节对齐是0x1000 （页 \_ 大小）的倍数。 例如 驱动程序 \_ 对齐 = 0x1000

以下 DDIs 列表未保留给系统使用可能会受到影响：

|                                                                                                      |
|------------------------------------------------------------------------------------------------------|
| DDI 名称                                                                                             |
| [**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)                                                          |
| [**ExAllocatePoolWithQuota**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)                                        |
| [**ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)                                  |
| [**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)                                            |
| [**ExAllocatePoolWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)                            |
| [**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)                        |
| [**ExInitializeLookasideListEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)                                |
| [**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)                                  |
| [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)          |
| [**MmAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)  |
| [**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)                          |
| [**MmCopyMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmcopymemory)                                                              |
| [**MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)                                                              |
| [**MmMapLockedPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)                                                      |
| [**MmMapLockedPagesSpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)                              |
| [**MmProtectMdlSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprotectmdlsystemaddress)                                    |
| [**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)                                        |
| [**ZwCreateSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)                                                        |
| [**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)                                                  |
| [**NtCreateSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)                                                        |
| [**NtMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)                                                  |
| [**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)                                    |
| NDIS                                                                                                 |
| [**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)                  |
| 存储                                                                                              |
| [**StorPortGetDataInBufferSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdatainbuffersystemaddress)             |
| [**StorPortGetSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetsystemaddress)                                     |
| [**ChangerClassAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassallocatepool)                                     |
| 显示                                                                                              |
| [*DxgkCbMapMemory*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_map_memory)                                                         |
| [**VideoPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportallocatepool)                                           |
| 音频微型端口                                                                                       |
| [**IMiniportDMus：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)                                        |
| [**IMiniportMidi：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-newstream)                                        |
| [**IMiniportWaveCyclic：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)                            |
| [**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-newmasterdmachannel)                      |
| [**IMiniportWavePci：： Newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)                                  |
| 音频端口类                                                                                     |
| [**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)                                                         |
| [**PcNewResourceList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)                                                     |
| [**PcNewResourceSublist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)                                               |
| IFS                                                                                                  |
| [**FltAllocatePoolAlignedWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatepoolalignedwithtag)                              |
| [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)                                                    |
| WDF                                                                                                  |
| [**WdfLookasideListCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdflookasidelistcreate)                                             |
| [**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)                                                           |
| [**WdfDeviceAllocAndQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryproperty)                             |
| [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)                         |
| [**WdfFdoInitAllocAndQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)                           |
| [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)                       |
| [**WdfIoTargetAllocAndQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetallocandquerytargetproperty)             |
| [**WdfRegistryQueryMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerymemory)                                             |


## <a name="using-the-dgreadiness-tool"></a>使用 DGReadiness 工具

若要使用 DGReadiness 工具，请完成以下步骤：

-   **准备测试 PC**

    *启用基于虚拟化的代码完整性保护*-运行系统信息应用（msinfo32）。 查找以下项： "基于虚拟化的安全性"。 它应显示： "正在运行"。

    另外，还提供了一个 WMI 接口，用于检查如何使用可用于在 PowerShell 中显示信息的管理工具。

    ```console
    Get-CimInstance –ClassName Win32_DeviceGuard –Namespace root\Microsoft\Windows\DeviceGuard
    ```

    *禁用 "Device guard"* -请注意，运行准备工具时，必须在测试中的 PC 上禁用 "device guard"，因为它可能会阻止加载驱动程序，并且驱动程序将不能用于测试。

    *（可选）启用测试签名*-若要允许安装未签名的开发驱动程序，您可能希望使用 BCDEdit 启用测试签名。

    ```console
    bcdedit /set TESTSIGNING ON
    ```

-   **安装测试驱动程序**

    在目标测试电脑上安装所需的测试驱动程序。

    **重要提示** 测试开发驱动程序并完成任何代码问题后，请重新测试最终的生产驱动程序。 此外，使用 HLK 测试驱动程序。 有关详细信息，请参阅[虚拟机监控程序代码完整性准备情况测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/b972fc52-2468-4462-9799-6a1898808c86)。



-   **安装 DGReadiness 工具**

    **警告**  
    由于 DGReadiness 工具更改注册表值，可能会影响安全启动等功能，因此请使用不包含任何数据或应用程序的测试 PC。 运行测试后，你可能需要重新安装 Windows 以重新建立所需的安全配置。

    1. 从此处下载此工具： [Device Guard 和 Credential Guard 硬件准备工具](https://www.microsoft.com/download/details.aspx?id=53337)。

    2. 在目标测试计算机上解压缩工具。

-   **将 PowerShell 配置为允许执行未签名的脚本。**

    准备工具是一个 PowerShell 脚本。 若要使用准备工具脚本，请打开管理员 PowerShell 脚本。

    如果尚未将执行策略设置为允许运行脚本，则应手动设置该策略，如下所示。

    ```powershell
    Set-ExecutionPolicy Unrestricted
    ```

-   **运行准备工具以启用要求 HVCI**

    1. 在 Powershell 中，找到要将准备工具解压缩到的目录。

    2. 运行准备工具以启用要求 HVCI。

    ```powershell
    DG_Readiness_Tool.ps1 -Enable HVCI
    ```

    3. 当定向时，重新启动 PC。

-   **运行脚本以评估要求 HVCI 功能**

    1. 运行准备工具以评估驱动程序支持要求 HVCI 的能力。

    ```powershell
    DG_Readiness_Tool.ps1 -Capable HVCI
    ```

-   **计算输出**

    屏幕的输出为彩色编码。

    |                   |                                                                                                   |
    |-------------------|---------------------------------------------------------------------------------------------------|
    | 红色-错误      | 元素缺失或未配置，将阻止启用和使用 DG/CG。                |
    | 黄色-警告 | 此设备可用于启用和使用 DG/CG，但不会有更多的安全优势。 |
    | 绿色-消息  | 此设备完全符合 DG/CG 要求。                                           |

    除了屏幕输出之外，默认情况下，具有详细输出的日志文件位于 C： \\ DGLogs

    在该工具的输出中有5个步骤（或部分）。 步骤1包含驱动程序兼容性信息。

    ```text
     ====================== Step 1 Driver Compat ====================== 
    ```

    绿色显示的驱动程序没有标识要求 HVCI 兼容性问题。 如果你对评估特定驱动程序感兴趣，则如果驱动程序名称显示为绿色并且处于活动状态且已加载，则它已通过要求 HVCI 兼容性测试。

    在日志的末尾找到如下所示的 "不兼容的要求 HVCI 内核驱动程序模块" 一节。

    ```text
    InCompatible HVCI Kernel Driver Modules found

    Module: TestDriver1.sys
        Reason: section alignment failures:             9
    Module: TestDriver2.sys
        Reason: execute pool type count:                3
    ```

    在上面所示的示例中，两个驱动程序被标识为不兼容。 TestDriver1 的内存部分对齐失败，TestDriver2 具有配置为使用可执行内存区域的池。

    使用！ verifier 调试器扩展时，还可以使用7种类型的设备驱动程序不兼容的统计信息。 有关！ verifier 扩展的详细信息，请参阅[**！ verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)。

    ```text
            Execute Pool Type Count:                3
            Execute Page Protection Count:          0
            Execute Page Mapping Count:             0
            Execute-Write Section Count:            0
            Section Alignment Failures:             0
            Unsupported Relocs Count:               0
            IAT in Executable Section Count:        0
    ```

使用下表来解释输出，并确定需要进行哪些驱动程序代码更改以修复不同类型的要求 HVCI 不兼容。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>

<tr class="odd">
<td align="left"><strong>警告</strong></td>
<td align="left"><strong>清偿</strong></td>
</tr>

<tr class="even">
<td align="left"><p>执行池类型</p></td>
<td align="left"><p>调用方指定了可执行的池类型。 调用请求可执行内存的内存分配函数。</p>
<p>请确保所有池类型都包含不可执行的 NX 标志。</p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>执行页面保护</p></td>
<td align="left"><p>调用方指定了可执行页保护。</p>
<p>指定 "无执行" 页保护掩码。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>执行页面映射</p></td>
<td align="left"><p>调用方指定了可执行的内存描述符列表（MDL）映射。</p>
<p> 请确保使用的掩码包含 MdlMappingNoExecute。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[MmGetSystemAddressForMdlSafe](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)">MmGetSystemAddressForMdlSafe</a></p>
</td>
</tr>

<tr class="odd">
<td align="left"><p>执行写入部分</p></td>
<td align="left"><p>映像包含可执行文件和可写部分。</p>
</td>
</tr>

<tr class="even">
<td align="left"><p>节对齐失败</p>
</td>
<td align="left"><p>图像包含不是页面对齐的部分。</p>
<p>节对齐必须是0x1000 （PAGE_SIZE）的倍数。 例如 DRIVER_ALIGNMENT = 0x1000</p></td>
</tr>


<tr class="even">
<td align="left"><p>可执行部分中的 IAT</p></td>
<td align="left"><p>导入地址表（IAT）不应为内存的可执行部分。</p>
<p>当 IAT 位于内存的读取和执行（RX）中时，会出现此问题。 这意味着 OS 将不能写入 IAT 来为所引用的 DLL 设置正确的地址。 </p>
<p> 出现这种情况的一种方法是在代码链接中使用<a href="https://docs.microsoft.com/cpp/build/reference/merge-combine-sections" data-raw-source="[/MERGE (Combine Sections)](https://docs.microsoft.com/cpp/build/reference/merge-combine-sections)">/merge （合并节）</a>选项。 例如，如果将. rdata （只读初始化数据）与进行合并，则 IAT 可能会在内存的可执行部分中结束。  </p>
</td>
</tr>

</tbody>
</table>

---------

不支持的重定位

<p>在 Windows 10 中，版本1507到 Windows 10，版本1607，因为使用地址空间布局随机化（ASLR），因此可能会出现地址对齐和内存重定位问题。  操作系统需要将地址从链接器设置其默认基址的位置重定位到 ASLR 分配的实际位置。 此重定位不能跨页面边界。  例如，请考虑在页面中以 offset 0x3FFC 开始的64位地址值。 它的地址值与0x0003 偏移量重叠到下一页。 在 Windows 10 版本1703之前，不支持此类型的重叠重定位。</p>

<p>当全局结构类型变量初始值设定项具有指向另一个全局结构的未对齐指针时，可能会出现这种情况，这种情况下，链接器无法移动变量来避免跨越重定位。 链接器将尝试移动变量，但在某些情况下，它可能无法执行此操作（例如，具有较大的结构或不对齐的结构的大型数组）。 在适当的情况下，应使用<a href="https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking" data-raw-source="[/Gy (COMDAT)](https://docs.microsoft.com/cpp/build/reference/gy-enable-function-level-linking)">/gy （COMDAT）</a>选项组装模块，以允许链接器尽可能地对齐模块代码。</p>

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

在其他情况下，也可能会出现此问题。

---------

## <a name="script-customization"></a>脚本自定义

下面是 Regkeys 的列表及其用于自定义脚本的值，用于在没有 UEFI 锁定的情况下要求 HVCI 和 Credential Guard。

若要启用要求 HVCI 和 CG 而不使用 UEFI 锁：

```reg
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "EnableVirtualizationBasedSecurity" /t REG_DWORD /d 1 /f' 
REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard" /v "RequirePlatformSecurityFeatures" /t REG_DWORD /d 1 /f' 
```

## <a name="driver-verifier-code-integrity"></a>驱动程序验证程序代码完整性

使用驱动程序验证程序代码完整性选项标志（0x02000000）启用验证与此功能的符合性的额外检查。 若要从命令行启用此项，请使用以下命令。

```console
verifier.exe /flags 0x02000000 /driver <driver.sys>
```

若要在使用验证程序 GUI 时选择此选项，请选择 "*创建自定义设置*（对于代码开发人员）"，选择 "*下一步*"，然后选择 "_代码完整性检查_"。

可以使用验证器命令行/query 选项显示当前的驱动程序验证程序信息。

```console
verifier /query
```
