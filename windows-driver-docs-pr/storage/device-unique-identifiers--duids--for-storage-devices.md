---
title: 存储设备的设备唯一标识符 (DUID)
description: 存储设备的设备唯一标识符 (DUID)
ms.assetid: 3846961c-5b75-4a1b-bced-601fc25bf071
keywords:
- 存储驱动程序 WDK、 Duid
- Duid WDK 存储
- 设备唯一的 Id WDK 存储
- 设备 Id WDK 存储
- 标识符 WDK 存储
- 序列号 WDK 存储
- 设备布局签名 WDK 存储
- 签名 WDK，存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80bcc5b28c1ea570fc637a3381f61d3af7107c1c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368291"
---
# <a name="device-unique-identifiers-duids-for-storage-devices"></a>存储设备的设备唯一标识符 (DUID)


当文件系统体系结构变得更加复杂时，操作系统组件数执行乘法运算，并通过越来越多地各种硬件和软件路径的发起程序访问存储目标，技术来识别存储设备变得不能满足需要。

例如，插即用 (PnP) 管理器将生成[的实例标识符 (ID)](https://docs.microsoft.com/windows-hardware/drivers/install/instance-ids)为计算机中的每个设备。 ID 对应于单个设备节点中每个实例[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)，唯一标识设备，如果设备处于同一位置。 当计算机重新启动，但它们不会保持相同如果将设备移到其他总线或另一台计算机时，持久保存实例 Id。 因此，实例 Id 是存储区域网络 (San) 中的应用程序和某些较新系统组件，如 Windows Vista 诊断服务，分布式存储的环境中运行的不足。 当硬盘磁盘驱动器预测智能故障时，会生成诊断服务的事件。 此事件必须包含唯一标识问题的硬盘的磁盘可能已在所有计算机上并可以将它附加到的所有总线上的标识符。 实例 Id 和任何其他[设备标识字符串](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)不适用于此目的。

某些应用程序和系统服务，例如 Microsoft 群集服务 (MSCS) 和分区管理器中，使用设备布局签名 ([**存储\_设备\_布局\_签名** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/ns-storduid-_storage_device_layout_signature)) 来唯一标识在群集中的存储设备。 但是，设备布局签名是为此，在某些情况下，不能满足需要，包括以下限制：

-   签名可能会更改或清除。

-   如果设备不旋转，或具有访问这些扇区的问题所在签名，签名可能不可用。

-   该签名是由另一个群集节点保留磁盘的情况下不可用。 MSCS 可以读取运行 MSCS 的节点与相关联的磁盘驱动器的布局。 软件必须访问不同的群集节点中的磁盘必须使用磁盘布局签名的替代方法。

-   驱动器布局签名不能帮助区分的逻辑单元号 (LUN) 和它的快照。 LUN 和它的快照具有相同的内容，因为其驱动器布局签名将是相同的。

序列号有时是一种可靠的技术来唯一地标识不依赖于设备的位置的存储设备。 序列号通常是作为设备的查询数据的一部分提供。 发起程序可以查询使用的查询数据[ **IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求和端口驱动程序报告中的查询的结果[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)结构。 但是，此方法无法帮助标识设备，例如磁带驱动器，不会报告查询数据。

### <a name="span-iddeviceuniqueidentifiersduidsspanspan-iddeviceuniqueidentifiersduidsspandevice-unique-identifiers-duids"></a><span id="device_unique_identifiers__duids_"></span><span id="DEVICE_UNIQUE_IDENTIFIERS__DUIDS_"></span>设备的唯一标识符 (Duid)

随着技术的发展，用于唯一标识设备通常技术变得过时，因为 Microsoft 已开发了称为设备唯一 ID (DUID) 是可扩展的并且，可以将合并新技术来识别为他们的设备使用设备 ID 格式变为可用。

由定义;，为 DUID [**存储\_设备\_UNIQUE\_标识符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/ns-storduid-_storage_device_unique_identifier)结构，并且此结构的第一个版本 (DUID\_版本\_1) 包括以下标识符的组合：

<span id="STORAGE_DEVICE_ID_DESCRIPTOR"></span><span id="storage_device_id_descriptor"></span>[**存储\_设备\_ID\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_id_descriptor)  
存储\_设备\_ID\_描述符结构包含从设备的重要产品数据 (VPD) 页 0x83 提取的标识符。 通常情况下，只有 SCSI 和光纤通道设备支持此页。 集成驱动电子设备 (IDE) 和通用串行总线 (USB) 设备，IEEE 1394 驱动器和 RAID 控制器不提供页 0x83。

<span id="STORAGE_DEVICE_DESCRIPTOR"></span><span id="storage_device_descriptor"></span>[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)  
存储\_设备\_描述符结构包含其他查询数据，包括中的单元序列号的偏移量**SerialNumberOffset**成员。 序列号的格式设置为可变长度**NULL**-结尾的字符串。 如果符合 SCSI 的存储设备，端口驱动程序将尝试从 VPD 可选单元序列号页 （页 0x80） 提取序列号。 如果存储设备是一个 IDE 设备，端口驱动程序将生成序列号从设备的标识数据。

<span id="STORAGE_DEVICE_LAYOUT_SIGNATURE"></span><span id="storage_device_layout_signature"></span>[**存储\_设备\_布局\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/ns-storduid-_storage_device_layout_signature)  
存储\_设备\_布局\_签名包含设备布局签名。

更多的数据将添加到 Duid 在将来版本。

Duid 不具有固定的大小，因此利用了 Duid （称为 DUID 使用者） 的软件必须获取的大小从 DUID**大小**的存储区的成员\_设备\_UNIQUE\_标识符结构。 DUID 版本现已推出 Vers * * * 此相同结构的离子成员。

某些设备不提供足够的信息系统保证设备的 DUID 足够唯一适用于所有使用和所有 DUID 客户。 如果操作系统可以从设备的 VPD 检索唯一 Id，它可以创建足够对于是唯一的;，为 DUID 的所有使用者 DUID。 如果系统必须 DUID 从设备布局签名单独创建，;，为 DUID 将足够唯一，但对于某些 DUID 使用者，但没有为其他。

系统会尝试创建具有以下特征 DUID:

-   DUID 保持不变时操作系统重启。

-   DUID 保持不变，即使设备从到另一台计算机、 一个适配器添加到另一个或一个通道移动到另一个。

-   DUID 标识设备和未媒体。 这一区别很重要的具有可移动介质的驱动器。

-   多路径在系统上，;，为 DUID 是相同的所有输入/输出路径。

Duid 具有以下限制：

-   Duid 通常包含无法显示的二进制内容。

-   Duid 并不总是**null**-已终止。 DUID 使用者必须检查**大小**的成员[**存储\_设备\_布局\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/ns-storduid-_storage_device_layout_signature)结构确定 DUID 的长度。

-   DUID 使用者必须使用[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids) Duid 比较而不是将其逐字节进行比较。

-   *枚举器*一定不要尝试使用 Duid 来标识用于插即用 (PnP) 设备对象。 多路径的系统可以有多个共享同一 DUID 的设备。 但对于即插即用，设备 Id 必须是唯一的。

发起程序可以查询的 DUID 信息数据使用[ **IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求使用的属性 ID **StorageDeviceUniqueIdProperty**。

### <a name="span-idhowtocompareduidsspanspan-idhowtocompareduidsspanhow-to-compare-duids"></a><span id="how_to_compare_duids"></span><span id="HOW_TO_COMPARE_DUIDS"></span>如何比较 Duid

DUID 使用者必须使用[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids) Storduids.h，来比较两个 Duid 中定义的例程。 **CompareStorageDuids**将返回[ **DUID\_匹配\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/ne-storduid-_duid_match_status)值，该值指示两个 Duid 是否匹配。 如果操作成功， **CompareStorageDuids**返回以下值之一：

<span id="DuidExactMatch"></span><span id="duidexactmatch"></span><span id="DUIDEXACTMATCH"></span>**DuidExactMatch**  
两个 Duid 中的所有字段完全都匹配。

<span id="DuidSubIdMatch"></span><span id="duidsubidmatch"></span><span id="DUIDSUBIDMATCH"></span>**DuidSubIdMatch**  
DUID 由若干子 Id 组成。 与至少一个子 Id 相匹配，并且两个 Duid 可能表示同一个设备。 设备固件更新时，它可能会获取新的标识符，这将更改的设备的 DUID 组合。 如果 DUID 使用者相比较的设备与新的 DUID，旧 DUID [ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)可能返回**DuidSubIdMatch**而不是**DuidExactMatch**。 这是基于子 ID 有效匹配项的示例。 DUID 使用者必须选择是否将接受**DuidSubIdMatch**返回值作为匹配项或不匹配，具体取决于 DUID 使用者的要求。

<span id="DuidNoMatch"></span><span id="duidnomatch"></span><span id="DUIDNOMATCH"></span>**DuidNoMatch**  
序列号不匹配，并从页面的重要产品数据 (VPD) 83 h 的唯一子 id 均不匹配。

除了以上值之外[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)可能会返回各个错误代码。

[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)例程使用以下算法来比较两个 Duid:

1.  检查完全匹配。 如果所有 Duid 中的数据，Duid 匹配完全匹配和[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)返回**DuidExactMatch**。 否则，继续进行下一次检查。

2.  检查 VPD 标识符。 如果任何唯一子 Id 匹配，Duid 匹配并[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)返回**DuidSubIdMatch**。 如果任何子 Id 匹配，或者设备不提供 VPD 的唯一标识符，继续进行下一次检查。

3.  检查单元序列号。 如果供应商 ID、 产品 ID 和序列号相同，Duid 匹配并[ **CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)返回**DuidSubIdMatch**。 如果任何这些值都不匹配或设备不提供这些值，则继续下一次检查。

4.  检查驱动器布局签名。 如果两个 Duid 驱动器布局签名匹配，Duid 匹配并[**CompareStorageDuids** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storduid/nf-storduid-comparestorageduids)返回**DuidSubIdMatch**。 如果驱动器签名不匹配，或者系统无法读取设备的驱动器布局签名，Duid 不匹配并**CompareStorageDuids**返回**DuidNoMatch**。

 

 




