---
title: COSA 概述
description: COSA 概述
ms.assetid: 45D69B8D-69C1-488B-AC52-D8DEB337F878
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e852750541d155843bbd6651a53974301f70f191
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563844"
---
# <a name="cosa-overview"></a>COSA 概述

COSA，或国家/地区和运算符设置资产是移动操作员 (MOs) 使用在 Windows 10，版本 1703年和更高版本的移动宽带 Windows 设备预配的新格式。 现有 APN 数据库 (apndatabase.xml) 从 Windows 8、 Windows 8.1 和 Windows 10 版本 1703年之前已转换为 COSA，这是通过新的预配框架 ingestible。 请注意，这些以前版本的 Windows 将继续使用较旧的 APN 数据库预配桌面设备。

有关较旧的 APN 数据库的详细信息，请参阅[APN 数据库概述](apn-database-overview.md)。

若要查看可以在桌面 COSA 中配置的可用设置 MOs 列表，请参阅[桌面 COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

## <a name="faq"></a>常见问题

- [MOs 可以 COSA 中指定的设置是什么？](#settings)
- [哪些事件触发新 MO 设置应用的程序？](#events)
- [COSA 使用调制解调器从哪些 sim 卡信息？](#SIMinfo)
- [是否有一种算法来执行最佳的 APN 匹配？](#APNmatch)
- [Where COSA 数据库存储，并可以对其进行直观地检查等 apndatabase.xml？](#location)
- [当设备从 Windows 10，版本 1607年 （或更早版本） 更新到 Windows 10，版本 1703年时，会发生什么情况？自定义或手动创建 APNs 迁移？他们是否仍有优先级通过从数据库的默认值？](#update)

### <a href="" id="settings"></a> MOs 可以 COSA 中指定的设置是什么？

设置很大程度上是哪些 MOs apndatabase.xml，具有少量例外和新添加的内容中配置相同。 有关详细信息，请参阅中的表[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。

### <a href="" id="events"></a> 哪些事件触发新 MO 设置应用的程序？

三个事件触发 Windows 配置引擎要查找的设置的更改： 

1.  插入或删除物理 SIM （ICCID 更改）
2.  Esim 卡 （ICCID 更改） 重新配置
3.  设备启动时

### <a href="" id="SIMinfo"></a> COSA 使用调制解调器从哪些 sim 卡信息？

月/MVNO 发现，Windows 会尝试在调制解调器使用 SPN 从 SIM COSA 数据库中进行的可用配置文件的最佳匹配项。

### <a href="" id="APNmatch"></a> 是否有一种算法来执行最佳的 APN 匹配？

在 Windows 10，版本 1703 之前, 的 Windows 版本 MOs 可以指定自动连接顺序。 Windows 10 版本 1703年及更高版本继续使用轮循机制方法通过所有可用的 APNs，但无法再用的算法以特定顺序。

### <a href="" id="location"></a> Where COSA 数据库存储，并可以对其进行直观地检查等 apndatabase.xml？

COSA 的 Windows 10 预配包 (.ppkg) 格式。 它是 Windows\Provisioning\COSA\Microsoft 文件夹中。 可以使用第三方工具，如 7-zip 文件管理器 ([www.7-Zip.org](https://go.microsoft.com/fwlink/p/?linkid=844795))，以直观地检查其内容。

请注意，OEM 扩展到 COSA，如果在设备图像中，指定 COSA\OEM 文件夹中。 有关详细信息，请参阅[自定义的国家/地区和运算符设置资产](https://msdn.microsoft.com/windows/hardware/commercialize/customize/desktop/customize-cosa)。

### <a href="" id="update"></a> 当设备从 Windows 10，版本 1607年或更早版本到 Windows 10，版本 1703年或更高版本更新时，会发生什么情况？ 自定义或手动创建 APNs 迁移？ 他们是否仍有优先级通过从数据库的默认值？

在升级后，COSA 替换 apndatabase.xml。 如果 APN 中以前的版本，预配是否自定义、 manual 或设备预配通过数据库，迁移升级到版本 1703年的一部分，并且设备将继续使用它进行连接而无需任何其他操作。 手动预配 APNs 仍会优先于从数据库的默认值和它们的操作一样在版本 1607年及更早版本。

