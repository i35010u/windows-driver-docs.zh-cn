---
title: 分区布局
description: 分区布局
ms.assetid: 59ac7ec7-1b96-4fe1-a221-d8422e60072d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00e9bcb94ae31e351e96735cc4c2ecd9e9001a5e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185709"
---
# <a name="windows-10-mobile-partition-layout"></a>Windows 10 移动版分区布局


在 Windows 10 移动版中，Microsoft 和硅供应商 (SV) 配置存储分区和分区大小。 必须对分区进行设计，使其足够大，可用于所有当前组件，并可在手机的生存期内接受更新。 在手机上设置分区大小时，更改大小的唯一方法是通过 reflashing 设备进行全新的完全刷新更新，这将擦除电话上的所有数据。

手机的存储子系统必须符合 [Windows 10 移动版最低硬件要求的 "2.2：内存" 部分](/windows-hardware/design/minimum/minimum-hardware-requirements-overview#section_2.0_-_minimum_hardware_requirements_for_windows_10_mobile)中指定的要求。

<div class="alert">
<strong>注意：</strong>   Oem 不能在 Microsoft 设计的布局中添加、删除或修改分区。 这有助于确保电话上的所有软件和配置数据都可以通过电话更新提供服务。 OEM 组件通常内置于主 OS 分区中， (用于预先加载的应用程序和本机服务) ，数据分区 (用于预加载映射) 或设备预配分区 (用于特定于设备的只读配置数据) 。
</div>
 

## <a name="span-idpartition_listspanspan-idpartition_listspanspan-idpartition_listspanpartition-list"></a><span id="Partition_list"></span><span id="partition_list"></span><span id="PARTITION_LIST"></span>分区列表


下图显示了所需的存储分区。

![分区布局](images/oem-bringup-partitionlayout.png)

## <a name="span-idpartition_requirementsspanspan-idpartition_requirementsspanspan-idpartition_requirementsspanpartition-requirements"></a><span id="Partition_requirements"></span><span id="partition_requirements"></span><span id="PARTITION_REQUIREMENTS"></span>分区要求


下表总结了每个分区的要求。 所有大小均为逻辑;存储媒体上消耗的实际空间可能会有所不同。 在定义系统分区的大小时 (包含除用户数据分区和 SD 卡) 之外的所有分区时，硅供应商必须符合每个分区的可用空间要求。 这包括但不限于软件资产，例如其他语言。 此要求是必需的，并且是必需的，以确保可以在电话的生存期内对其进行更新。

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
<th align="left">分区</th>
<th align="left">目录</th>
<th align="left">文件系统</th>
<th align="left">装入点</th>
<th align="left">已加密</th>
<th align="left">大小</th>
<th align="left">为将来的更新保留的可用空间</th>
<th align="left">Owner</th>
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
<td align="left"><p>不适用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="even">
<td align="left"><p>SV 分区</p></td>
<td align="left"><p>UEFI 固件和其他 SV 特定的分区</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>无装入点</p></td>
<td align="left"><p>可能</p></td>
<td align="left"><p>变量</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>SV/OEM</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EFI 系统分区</p></td>
<td align="left"><p>启动管理器，启动配置数据库，UEFI 应用程序</p></td>
<td align="left"><p>FAT</p></td>
<td align="left"><p>C:\ESP</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>32 MB (最小) </p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="even">
<td align="left"><p>故障转储分区 (仅存在于非零售映像) </p></td>
<td align="left"><p>故障转储中的数据</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C:\CrashDump</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>变量-此分区的大小取决于用于生成映像的 OEMInput 文件中的 <strong>SOC</strong> 元素的值。</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="odd">
<td align="left"><p>主 OS (启动分区) </p></td>
<td align="left"><p>OS，更新 OS，系统注册表配置单元，OEM 预加载应用程序</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C： &lt; /p&gt;</td>
<td align="left"><p>是</p></td>
<td align="left"><p>约 1.5 GB</p>
</td>
<td align="left"><p>250 MB</p>
</td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="even">
<td align="left"><p>数据分区</p></td>
<td align="left"><p>用户数据、用户注册表配置单元、应用程序、应用程序数据、页文件。</p></td>
<td align="left"><p>NTFS</p></td>
<td align="left"><p>C：\Data</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>其他分区未使用 eMMC 存储空间的剩余部分。 页面文件使用约 256 MB。</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SD 卡</p></td>
<td align="left"><p>用户数据 (音乐、图片等 ) </p></td>
<td align="left"><p>FAT/exFAT</p></td>
<td align="left"><p>变量</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>变量</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>Microsoft</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddevice_provisioning_partitionspanspan-iddevice_provisioning_partitionspanspan-iddevice_provisioning_partitionspandevice-provisioning-partition"></a><span id="Device_provisioning_partition"></span><span id="device_provisioning_partition"></span><span id="DEVICE_PROVISIONING_PARTITION"></span>设备预配分区

设备预配分区 (DPP) 包含特定设备的设置数据。 它通常在工厂地面进行校准，并包含产品验证密钥以及组件（如收音机和 GPS）的配置信息。 由于它是特定于设备的，因此将其从任何映像更新或 FFU 中排除。

此分区的大小应为 8 MB。

<div class="alert">
<strong>重要提示：</strong>   DPP 分区必须是布局中的第一个分区，以便在任何其他分区的大小随后发生更改时安全保护设置信息不被覆盖。
</div>

### <a name="span-idsilicon_vendor_partitionsspanspan-idsilicon_vendor_partitionsspanspan-idsilicon_vendor_partitionsspansilicon-vendor-partitions"></a><span id="Silicon_vendor_partitions"></span><span id="silicon_vendor_partitions"></span><span id="SILICON_VENDOR_PARTITIONS"></span>硅供应商分区

SV 可以为自己的组件定义分区。 其中一个分区是 UEFI (统一可扩展固件接口) 分区，其中包含一个 UEFI 应用程序可使用的一组基元系统操作的标准接口。 调制解调器数据还需要 SV 分区。


### <a name="span-idefi_system_partitionspanspan-idefi_system_partitionspanspan-idefi_system_partitionspanefi-system-partition"></a><span id="EFI_system_partition"></span><span id="efi_system_partition"></span><span id="EFI_SYSTEM_PARTITION"></span>EFI 系统分区

EFI 系统分区包含 Windows 启动管理器 (BootMgr) 和启动配置数据库 (BCD) 。 BootMgr 负责加载较高级别的操作系统，如主操作系统或更新操作系统。 此外，EFI 系统分区包含许多 UEFI 应用程序，如 FFU 应用程序和电池充电应用程序。

此分区的大小至少为 32 MB。

### <a name="span-idcrash_dump_partitionspanspan-idcrash_dump_partitionspanspan-idcrash_dump_partitionspancrash-dump-partition"></a><span id="Crash_dump_partition"></span><span id="crash_dump_partition"></span><span id="CRASH_DUMP_PARTITION"></span>故障转储分区

非零售映像包含故障转储分区，其中包含在手机意外重启时出现的故障转储数据。

此分区的大小取决于用于生成映像的 OEMInput 文件中的 **SOC** 元素的值。

### <a name="span-idmain_os_partitionspanspan-idmain_os_partitionspanspan-idmain_os_partitionspanmain-os-partition"></a><span id="Main_OS_partition"></span><span id="main_os_partition"></span><span id="MAIN_OS_PARTITION"></span>主 OS 分区

主 OS 分区（也称为启动分区）包含构成操作系统映像的所有组件。 这包括 OEM 自定义和预加载应用程序。

此分区大小取决于 OEM 自定义和预加载应用程序所使用的空间量。 

* **基线操作系统**：约 870 MB，但实际上操作系统的大小取决于多个变量，如图像中包含的语言数。 在具有压缩的主操作系统分区的 4 GB 手机上，操作系统大约比未压缩的 OS 小 20%-25%。
* **更新操作系统**：约 50 MB
* **OEM 预先加载的应用程序**：在第一次启动体验期间安装的应用程序最多支持 100 MB，在首次启动后安装的应用程序的剩余用户存储空间的5%
* **保留以供将来更新**：变量，具体取决于电话上的存储量。 有关详细信息，请参阅下一列。

通常，此分区中的可写文件数应限制为可能的最小值，以允许进行更新。 此分区包括保留空间，以允许因更新而增长：

-   在只有 4 GB 存储空间的手机上，在压缩主 OS 分区后，此分区的保留空间大约为 250 MB。

-   对于超过 4 GB 的存储和未压缩的主 OS 分区，该分区的保留空间大约为 250 MB。

<div class="alert">
<strong>注意：</strong>   通过使用设备平台 XML 文件中的<strong>AdditionalMainOSFreeSectorsRequest</strong>元素，oem 可以为将来的更新添加更多可用空间。
</div>


### <a name="span-iddata_partitionspanspan-iddata_partitionspanspan-iddata_partitionspandata-partition"></a><span id="Data_partition"></span><span id="data_partition"></span><span id="DATA_PARTITION"></span>数据分区

内部存储中的此分区存储用户数据、应用程序和应用程序状态。 分区大小会自动调整，以消耗 eMMC 上剩余的空间。

<div class="alert">
<strong>重要提示：</strong>   数据分区必须是布局中的最后一个分区。
</div>

### <a name="span-idsd_cardspanspan-idsd_cardspanspan-idsd_cardspansd-card"></a><span id="SD_card"></span><span id="sd_card"></span><span id="SD_CARD"></span>SD 卡

可移动用户数据分区指的是存储在 SD 卡上的数据。 SD 卡被视为单独的卷，用于存储特定类型的用户数据。 用户随时可以从系统中删除 SD 卡上的内容，因此不能包含对核心电话功能至关重要的信息。
