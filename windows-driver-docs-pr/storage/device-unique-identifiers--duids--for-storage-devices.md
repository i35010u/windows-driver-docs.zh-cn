---
title: 存储设备的设备唯一标识符 (DUID)
description: 存储设备的设备唯一标识符 (DUID)
ms.assetid: 3846961c-5b75-4a1b-bced-601fc25bf071
keywords:
- 存储驱动程序 WDK，Duid
- Duid WDK 存储
- 设备唯一 Id WDK 存储
- 设备 Id WDK 存储
- 标识符 WDK 存储
- 序列号 WDK 存储
- 设备布局签名 WDK 存储
- 签名 WDK，存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 632cfd4e6c28c945b36b5d301ca8ff2b55a04af1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845178"
---
# <a name="device-unique-identifiers-duids-for-storage-devices"></a>存储设备的设备唯一标识符 (DUID)


如果文件系统体系结构变得越来越复杂，操作系统组件的数量会成倍增加，并且发起程序通过越来越多的硬件和软件路径来访问存储目标，则识别存储设备的方法会变得不充分。

例如，即插即用（PnP）管理器为计算机中的每个设备生成一个[实例标识符（ID）](https://docs.microsoft.com/windows-hardware/drivers/install/instance-ids) 。 如果设备仍处于同一位置，则每个实例 ID 都对应于[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)中的单个设备节点并唯一地标识设备。 当计算机重新启动时，实例 Id 仍保持不变，但如果将设备移到不同的总线或其他计算机上，则它们不会保持不变。 因此，实例 Id 对于存储区域网络（San）中的应用程序和在具有分布式存储的环境中操作的一些较新的系统组件（例如 Windows Vista 诊断服务）而言不够用。 当硬盘驱动器预测到智能故障时，它会为诊断服务生成一个事件。 此事件必须包含一个标识符，该标识符可用于唯一标识磁盘可能位于的所有计算机上的故障硬盘以及可以附加到的所有总线。 出于此目的，实例 Id 和任何其他[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)都不够充分。

某些应用程序和系统服务（例如 Microsoft 群集服务（MSCS）和分区管理器）使用设备布局签名（[**存储\_设备\_布局\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_layout_signature)）来唯一标识存储设备聚集. 但在某些情况下，设备布局签名不足以实现此目的，并且具有以下限制：

-   签名可能会更改，也可能会被清除。

-   如果设备未旋转，或在访问签名所在的扇区时出现问题，则签名可能不可用。

-   如果磁盘已由其他群集节点保留，则该签名不可用。 MSCS 只能读取与 MSCS 正在其上运行的节点关联的磁盘的驱动器布局。 必须访问不同群集节点中的磁盘的软件必须使用磁盘布局签名的替代方法。

-   驱动器布局签名无法帮助区分逻辑单元号（LUN）及其快照。 由于 LUN 及其快照具有相同的内容，因此其驱动器布局签名将相同。

序列号有时是一种可靠的方法，用于唯一标识不依赖设备位置的存储设备。 序列号通常作为设备查询数据的一部分提供。 发起方可以使用[**IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求查询查询数据，端口驱动程序会在[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)结构中报告查询的结果。 但是，此方法不会帮助确定不报告查询数据的设备，如磁带驱动器。

### <a name="span-iddevice_unique_identifiers__duids_spanspan-iddevice_unique_identifiers__duids_spandevice-unique-identifiers-duids"></a><span id="device_unique_identifiers__duids_"></span><span id="DEVICE_UNIQUE_IDENTIFIERS__DUIDS_"></span>设备唯一标识符（Duid）

由于在技术发展时，用于唯一标识设备的方法通常会过时，因此，Microsoft 开发的设备 ID 格式是可扩展的，并且可以并入新的方法来识别设备变为可用。

DUID 由[**存储\_设备定义\_唯一\_标识符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_unique_identifier)结构，此结构的第一个版本（DUID\_版本\_1）包含以下标识符的组合：

<span id="STORAGE_DEVICE_ID_DESCRIPTOR"></span><span id="storage_device_id_descriptor"></span>[**存储\_设备\_ID\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_id_descriptor)  
存储\_设备\_ID\_描述符结构包含从设备重要产品数据（VPD）的页面0x83 中提取的标识符。 通常，只有 SCSI 和光纤通道设备支持此页。 集成驱动电子设备（IDE）和通用串行总线（USB）设备、IEEE 1394 驱动器和 RAID 控制器不提供页面0x83。

<span id="STORAGE_DEVICE_DESCRIPTOR"></span><span id="storage_device_descriptor"></span>[ **\_设备\_描述符的存储**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)  
存储\_设备\_描述符结构包含其他查询数据，其中包括**SerialNumberOffset**成员中的 unit 序列号偏移量。 序列号的格式为长度可变、以**NULL**结尾的字符串。 如果存储设备符合 SCSI 标准，则端口驱动程序将尝试从 VPD 的可选 "设备序列号" 页（页0x80）中提取序列号。 如果存储设备是 IDE 设备，则端口驱动程序将从设备的标识数据生成序列号。

<span id="STORAGE_DEVICE_LAYOUT_SIGNATURE"></span><span id="storage_device_layout_signature"></span>[ **\_设备\_布局\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_layout_signature)  
存储\_设备\_布局\_签名包含设备布局签名。

未来版本中将向 Duid 添加更多数据。

Duid 不具有固定大小，因此使用 Duid （称为 DUID 使用者）的软件必须从存储\_设备的**size**成员那里获取 DUID 大小\_唯一\_标识符结构。 可以在此同一结构的所有可用的中，使用该版本的 DUID。

某些设备并不为系统提供足够的信息来保证设备的 DUID 对于所有使用情况和所有 DUID 使用者而言都是足够唯一的。 如果操作系统可以从设备的 VPD 中检索唯一 Id，则可以为所有 DUID 使用者创建足够唯一的 DUID。 但是，如果系统必须单独从设备布局签名创建 DUID，则对于某些 DUID 使用者（而不是其他），DUID 将非常独特。

系统将尝试创建具有以下特征的 DUID：

-   操作系统重新启动时，DUID 保持不变。

-   即使将设备从一台计算机移动到另一台计算机，另一个适配器移到另一台计算机，或者在通道间移动时，DUID 仍保持不变。

-   DUID 标识设备而不是媒体。 这种区别对于具有可移动媒体的驱动器非常重要。

-   对于多路径系统，其所有 i/o 路径都是相同的。

Duid 具有以下限制：

-   Duid 通常包含无法显示的二进制内容。

-   Duid 并非始终以**null**结尾。 DUID 使用者必须检查[**存储\_设备\_布局\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ns-storduid-_storage_device_layout_signature)结构的**大小**成员，以确定 DUID 的长度。

-   DUID 使用者必须使用[**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)来比较 duid，而不是按字节对它们进行比较。

-   *枚举*器不能尝试使用 duid 来识别即插即用（PnP）用途的设备对象。 多路径系统可以有多个共享同一 DUID 的设备。 但对于 PnP，设备 Id 必须是唯一的。

发起程序可以使用[**IOCTL\_存储\_query\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求的属性 ID 为**STORAGEDEVICEUNIQUEIDPROPERTY**来查询 DUID 信息数据。

### <a name="span-idhow_to_compare_duidsspanspan-idhow_to_compare_duidsspanhow-to-compare-duids"></a><span id="how_to_compare_duids"></span><span id="HOW_TO_COMPARE_DUIDS"></span>如何比较 Duid

DUID 使用者必须使用 Storduids 中定义的[**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)例程来比较两个 duid。 **CompareStorageDuids**返回[ **\_匹配的 DUID\_状态值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/ne-storduid-_duid_match_status)，该值指示两个 duid 是否匹配。 如果操作成功，则**CompareStorageDuids**返回以下值之一：

<span id="DuidExactMatch"></span><span id="duidexactmatch"></span><span id="DUIDEXACTMATCH"></span>**DuidExactMatch**  
这两个 Duid 中的所有字段完全匹配。

<span id="DuidSubIdMatch"></span><span id="duidsubidmatch"></span><span id="DUIDSUBIDMATCH"></span>**DuidSubIdMatch**  
DUID 由若干子 Id 组成。 至少一个子 Id 匹配，而两个 Duid 可能表示相同的设备。 更新设备固件后，它可能会获取新的标识符，这将更改设备的 DUID 组合。 如果 DUID 使用者与新的 DUID 比较设备的旧 DUID， [**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)可能会返回**DuidSubIdMatch**而不是**DuidExactMatch**。 这是一个基于子 ID 的有效匹配的示例。 DUID 使用者必须选择是否将**DuidSubIdMatch**返回值视为匹配或不匹配，具体取决于 duid 使用者的要求。

<span id="DuidNoMatch"></span><span id="duidnomatch"></span><span id="DUIDNOMATCH"></span>**DuidNoMatch**  
序列号不匹配，并且不匹配重要产品数据（VPD）第83h 页中的唯一子 Id。

除了前面的值以外， [**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)可能还会返回各种错误代码。

[**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)例程使用以下算法来比较两个 duid：

1.  检查是否完全匹配。 如果 Duid 中的所有数据均匹配，则 Duid 将完全匹配， [**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)将返回**DuidExactMatch**。 否则，请继续下一次检查。

2.  检查 VPD 标识符。 如果任何唯一的子 Id 匹配，则 Duid match 和[**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)将返回**DuidSubIdMatch**。 如果没有匹配的子 Id 或设备未提供唯一的 VPD 标识符，请继续下一次检查。

3.  检查 unit 序列号。 如果供应商 ID、产品 ID 和序列号相同，则 Duid match 和[**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)将返回**DuidSubIdMatch**。 如果这些值都不匹配或设备未提供这些值，则继续下一次检查。

4.  检查驱动器布局签名。 如果两个 Duid 匹配的驱动器布局签名，则 Duid match 和[**CompareStorageDuids**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storduid/nf-storduid-comparestorageduids)将返回**DuidSubIdMatch**。 如果驱动器签名不匹配，或者系统无法读取设备的驱动器布局签名，则 Duid 不匹配，并且**CompareStorageDuids**将返回**DuidNoMatch**。

 

 




