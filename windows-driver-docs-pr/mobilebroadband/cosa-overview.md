---
title: COSA 概述
description: COSA 概述
ms.assetid: 45D69B8D-69C1-488B-AC52-D8DEB337F878
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dc4c16fd217ced9ab881a20ac388b189a50101f
ms.sourcegitcommit: 257850d61aa5d1db707dc2f30721319b650e47f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801173"
---
# <a name="cosa-overview"></a>COSA 概述

COSA 或国家/地区和操作员设置资产是移动运营商（MOs）在 Windows 10 版本1703及更高版本中使用的新格式，用于为移动宽带设置 Windows 设备。 1703之前的 windows 8、Windows 8.1 和版本中的现有 APN 数据库（apndatabase）已转换为 COSA，这是由新的预配框架 ingestible 的。 请注意，这些以前版本的 Windows 将继续使用较旧的 APN 数据库来预配桌面设备。

有关较旧 APN 数据库的详细信息，请参阅[APN 数据库概述](apn-database-overview.md)。

若要查看 MOs 可以在 desktop COSA 中配置的可用设置的列表，请参阅[DESKTOP COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

## <a name="faq"></a>常见问题解答

- [MOs 可以在 COSA 中指定哪些设置？](#settings)
- [哪些事件触发了新的 MO 设置的应用？](#events)
- [COSA 使用调制解调器的哪些 SIM 信息？](#SIMinfo)
- [是否有可使最大 APN 匹配的算法？](#APNmatch)
- [COSA 数据库存储在何处，可以在视觉上检查它（如 apndatabase）？](#location)
- [如果设备从 Windows 10 版本1607（或更低版本）更新到 Windows 10，版本1703，会发生什么情况？自定义或手动创建的 APNs 是否已迁移？它们是否仍具有数据库中默认值的优先级？](#update)
- [为什么**设置为按流量计费的连接**设置有时会从**Off**改为**打开**状态？](#metered)

### <a href="" id="settings"></a>MOs 可以在 COSA 中指定哪些设置？

这些设置在很大程度上与在 apndatabase 中配置的 MOs 相同，但有一些例外情况和新增功能。 有关详细信息，请参阅[规划桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)中的表。

### <a href="" id="events"></a>哪些事件触发了新的 MO 设置的应用？

三个事件触发 Windows 预配引擎以查找设置中的更改： 

1.  插入或删除物理 SIM （在 ICCID 中更改）
2.  重新配置 eSIM （在 ICCID 中更改）
3.  设备启动时

### <a href="" id="SIMinfo"></a>COSA 使用调制解调器的哪些 SIM 信息？

对于 MO/MVNO 发现，Windows 会尝试使用调制解调器中 SIM 的 SPN，使 COSA 数据库中的可用配置文件的最佳匹配。

### <a href="" id="APNmatch"></a>是否有可使最大 APN 匹配的算法？

在 Windows 10 版本1703之前的 Windows 版本中，MOs 可以指定自动连接顺序。 Windows 10 版本1703和更高版本通过所有可用的 APNs 继续使用轮循方法，但不再是算法所使用的特定顺序。

### <a href="" id="location"></a>COSA 数据库存储在何处，可以在视觉上检查它（如 apndatabase）？

COSA 的格式为 Windows 10 预配包（ppkg）。 它位于 Windows\Provisioning\COSA\Microsoft 文件夹中。 您可以使用第三方工具（如 7-Zip 文件管理器（[www.7-Zip.org](https://go.microsoft.com/fwlink/p/?linkid=844795)））来直观地检查其内容。

请注意，COSA 的 OEM 扩展（如果在设备映像中指定）位于 COSA\OEM 文件夹中。 有关详细信息，请参阅[自定义国家和操作员设置资产](https://docs.microsoft.com/windows-hardware/customize/desktop/customize-cosa)。

### <a href="" id="update"></a>如果设备从 Windows 10 版本1607或更早版本升级到 Windows 10，版本1703或更高版本，会发生什么情况？ 自定义或手动创建的 APNs 是否已迁移？ 它们是否仍具有数据库中默认值的优先级？

升级后，COSA 将替换 apndatabase。 如果在以前的版本中预配了某个 APN，无论是通过数据库进行自定义、手动还是设备预配，则会在升级到版本1703时迁移该接入点，并且设备将继续使用该接入点进行连接，而无需执行任何其他操作。 像在版本1607和更早版本中一样，手动预配 APNs 仍具有数据库默认值的优先级。

### <a href="" id="metered"></a>为什么 "设置为按流量计费的连接" 设置有时从**Off**更改为 "**打开**"？

Windows 操作系统的更新可能包括 COSA 数据库的更新。 如果更新了数据库，则设置引擎可能会删除手机网络配置文件。 当系统在安装数据库更新后重新启动时，设置引擎会重新安装手机网络配置文件。 此操作将用户设置重置为其默认值。 例如，**将设置为按流量计费**，从**Off**更改为**On**。 此行为是设计使然。
