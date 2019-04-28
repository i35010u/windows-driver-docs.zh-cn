---
title: 分区布局
description: 分区布局
ms.assetid: 59ac7ec7-1b96-4fe1-a221-d8422e60072d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c7fccb17923cebd1236b368820130abb71900d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337517"
---
# <a name="windows-10-mobile-partition-layout"></a>Windows 10 移动版的分区布局


在 Windows 10 移动版、 Microsoft 和硅供应商 (SV) 配置的存储分区和分区大小。 必须设计分区，以便它们足够大，针对所有当前组件和接受更新的手机的整个生命周期。 已在手机上设置的分区大小后，更改大小的唯一方法是通过重新刷新清理完整闪存的更新，这将擦除所有数据在手机上的设备。

在手机的存储子系统中指定的要求必须符合[部分 2.2:Windows 10 移动版的最低硬件要求的内存，](https://msdn.microsoft.com/library/windows/hardware/dn915086.aspx#section_2.0_-_minimum_hardware_requirements_for_windows_10_mobile)。

<div class="alert">
<strong>注意：</strong>  Oem 可能不添加、 删除或修改由 Microsoft 和 SV 设计布局中的分区。 这有助于确保在手机上的所有软件和配置数据可以为电话更新提供都服务。 OEM 组件通常内置于主要的 OS 分区 （适用于预加载应用程序和本机服务），数据分区 （适用于数据预加载映射等） 或在设备预配分区 （适用于特定于设备的只读配置数据）。
</div>
 

## <a name="span-idpartitionlistspanspan-idpartitionlistspanspan-idpartitionlistspanpartition-list"></a><span id="Partition_list"></span><span id="partition_list"></span><span id="PARTITION_LIST"></span>分区列表


下图显示了所需的存储分区。

![分区布局](images/oem-bringup-partitionlayout.png)

## <a name="span-idpartitionrequirementsspanspan-idpartitionrequirementsspanspan-idpartitionrequirementsspanpartition-requirements"></a><span id="Partition_requirements"></span><span id="partition_requirements"></span><span id="PARTITION_REQUIREMENTS"></span>分区要求


下表总结了为每个分区的要求。 所有大小都是逻辑;实际占用的存储媒体上的空间可能会有所不同。 定义系统分区 （其中包括除用户数据分区和 SD 卡之外的所有分区） 的大小，硅供应商必须遵守每个分区的可用空间要求。 这包括但不限于等其他语言的软件资产。 此要求是必需的和必要的以确保其生存期内，可以更新电话。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Partition</th>
<th align="left">目录</th>
<th align="left">文件系统</th>
<th align="left">装入点</th>
<th align="left">Encrypted</th>
<th align="left">大小</th>
<th align="left">保留供将来的更新的可用空间</th>
<th align="left">所有者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DPP</p></td>
<td align="left"><p>设备预配数据</p></td>
<td align="left"><p>FAT</p></td>
<td align="left"><p>C:\DPP</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>8 MB</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="even">
<td align="left"><p>SV 分区</p></td>
<td align="left"><p>UEFI 固件和其他特定于 SV 的分区</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>没有装入点</p></td>
<td align="left"><p>可能</p></td>
<td align="left"><p>变量</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>SV/OEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EFI 系统分区</p></td>
<td align="left"><p>启动管理器、 引导配置数据库、 UEFI 应用程序</p></td>
<td align="left"><p>FAT</p></td>
<td align="left"><p>C:\ESP</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>32 MB （最低）</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="even">
<td align="left"><p>崩溃转储分区 （仅非零售映像存在）</p></td>
<td align="left"><p>故障转储中的数据</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:\CrashDump</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>变量-此分区的大小取决于的值<strong>SOC</strong> OEMInput 文件用于生成映像中的元素。</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Main OS （启动分区）</p></td>
<td align="left"><p>OS 更新系统注册表配置单元、 OEM 预加载应用程序的 OS</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:&lt;/p&gt;</td>
<td align="left"><p>是</p></td>
<td align="left"><p>约为 1.5 GB</p>
</td>
<td align="left"><p>250 MB</p>
</td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="even">
<td align="left"><p>数据分区</p></td>
<td align="left"><p>用户数据、 用户注册表配置单元中，应用程序、 应用程序数据、 页面文件。</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:\Data</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>EMMC 存储未由其他分区的其余部分。 大约 256 MB 用于页面文件。</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SD 卡</p></td>
<td align="left"><p>用户数据 （如音乐、 图片等）。</p></td>
<td align="left"><p>FAT/exFAT</p></td>
<td align="left"><p>变量</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>变量</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeviceprovisioningpartitionspanspan-iddeviceprovisioningpartitionspanspan-iddeviceprovisioningpartitionspandevice-provisioning-partition"></a><span id="Device_provisioning_partition"></span><span id="device_provisioning_partition"></span><span id="DEVICE_PROVISIONING_PARTITION"></span>设备预配分区

设备预配分区 (DPP) 包含特定设备的设置数据。 它通常校准工厂地板上并且包含产品验证密钥以及组件，如单选和 GPS 的配置信息。 因为它是特定于设备，会从任何映像的更新或 FFU 中排除。

此分区应为 8 MB 的大小。

<div class="alert">
<strong>重要说明：</strong> DPP 分区必须为布局中的第一个分区，因此作为到安全防范措施覆盖设置的信息应该的任何其他分区大小随后更改。
</div>

### <a name="span-idsiliconvendorpartitionsspanspan-idsiliconvendorpartitionsspanspan-idsiliconvendorpartitionsspansilicon-vendor-partitions"></a><span id="Silicon_vendor_partitions"></span><span id="silicon_vendor_partitions"></span><span id="SILICON_VENDOR_PARTITIONS"></span>硅供应商分区

SV 可以定义自己的组件的分区。 这些分区中的一个是 UEFI （统一可扩展固件接口） 分区，其中包含一基元的 UEFI 应用程序可以使用的系统操作的标准接口。 调制解调器数据还需要一个 SV 分区。


### <a name="span-idefisystempartitionspanspan-idefisystempartitionspanspan-idefisystempartitionspanefi-system-partition"></a><span id="EFI_system_partition"></span><span id="efi_system_partition"></span><span id="EFI_SYSTEM_PARTITION"></span>EFI 系统分区

EFI 系统分区包含 Windows 启动管理器 (BootMgr) 和引导配置数据库 (BCD)。 BootMgr 负责加载更高级别的操作系统，如主操作系统或更新操作系统。 此外，EFI 系统分区包含数 UEFI 应用程序，例如 FFU 应用程序和电池充电应用程序。

此分区应至少 32 MB 的大小。

### <a name="span-idcrashdumppartitionspanspan-idcrashdumppartitionspanspan-idcrashdumppartitionspancrash-dump-partition"></a><span id="Crash_dump_partition"></span><span id="crash_dump_partition"></span><span id="CRASH_DUMP_PARTITION"></span>崩溃转储分区

非零售映像包含一个故障转储分区，其中包含从电话意外重启时出现的故障转储数据。

此分区的大小取决于的值**SOC** OEMInput 文件用于生成映像中的元素。

### <a name="span-idmainospartitionspanspan-idmainospartitionspanspan-idmainospartitionspanmain-os-partition"></a><span id="Main_OS_partition"></span><span id="main_os_partition"></span><span id="MAIN_OS_PARTITION"></span>主操作系统分区

主要 OS 分区，也称为引导分区包含的所有组件构成的操作系统映像。 这包括 OEM 自定义和预加载应用程序。

此分区的此大小取决于由 OEM 自定义和预加载应用程序使用的空间量。 

* **基准 OS**: ~ 870 MB，尽管在现实中的操作系统的大小取决于许多变量，如语言数量包括在映像中。 4 GB 在手机上使用压缩的主要 OS 分区，OS 是大约 20%-25%小于未压缩的 OS。
* **更新 OS**: ~ 50 MB
* **OEM 预加载应用程序**： 在首次启动体验，向上 5%的安装后首次启动体验的应用程序的剩余用户存储过程中安装的应用程序的最大 100 MB
* **保留供将来的更新**:变量，具体取决于在手机上的存储量。 请参阅下一步列了解详细信息。

一般情况下，此分区中的可写文件数应限制为最小的可能以允许足够的空间用于更新。 此分区包括保留的空间以便由于更新而增长：

-   在手机上使用只有 4 GB 的存储，此分区之后压缩主操作系统分区具有大约 250 MB 的保留空间。

-   在手机上使用超过 4 GB 的存储和未压缩的主操作系统分区，此分区都有大约 250 MB 的保留空间。

<div class="alert">
<strong>注意：</strong>  Oem 可以通过添加更多可用空间为将来的更新<strong>AdditionalMainOSFreeSectorsRequest</strong>设备平台 XML 文件中的元素。
</div>


### <a name="span-iddatapartitionspanspan-iddatapartitionspanspan-iddatapartitionspandata-partition"></a><span id="Data_partition"></span><span id="data_partition"></span><span id="DATA_PARTITION"></span>数据分区

此分区在内部存储中的存储用户数据、 应用和应用程序状态。 分区的大小自动调整，以使用 eMMC 上的空间的其余部分。

<div class="alert">
<strong>重要说明：</strong> 数据分区必须在布局中的最后一个分区。
</div>

### <a name="span-idsdcardspanspan-idsdcardspanspan-idsdcardspansd-card"></a><span id="SD_card"></span><span id="sd_card"></span><span id="SD_CARD"></span>SD 卡

可移动的用户数据分区是指存储在 SD 卡上的数据。 SD 卡视为一个单独的卷用于存储某些类型的用户数据。 SD 卡上的内容可以从系统中删除由用户在任何时间，因此不能包含对核心电话功能至关重要的信息。
 


