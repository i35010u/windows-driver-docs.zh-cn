---
title: Windows 8 中的网络内核调试支持的以太网 NIC
description: 您可以执行操作时目标计算机正在运行 Windows 8 内核调试通过以太网网络电缆。 目标计算机必须具有支持的网络接口卡 (NIC) 或网络适配器。
ms.assetid: 92FEEBAF-9978-4BDE-BB4F-81454D84A7E7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1973d4d39270d6a9ac25f9badfedc45b1adfccb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562565"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-8"></a>Windows 8 中的网络内核调试支持的以太网 NIC


您可以执行操作时目标计算机正在运行 Windows 8 内核调试通过以太网网络电缆。 目标计算机必须具有支持的网络接口卡 (NIC) 或网络适配器。

在内核调试，期间调用运行调试器的计算机*主机计算机*，和正在调试的计算机称为*目标计算机*。 若要执行操作[内核调试通过网络电缆](setting-up-a-network-debugging-connection.md)，目标计算机必须具有支持的网络适配器。 当目标计算机正在运行 Windows 8 时，此处列出的网络适配器支持内核调试。

**请注意**  支持的 Windows 8.1 的内核调试网络适配器的列表，请参阅[对于 Windows 8.1 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)。

 

## <a name="span-idsystemrequirementsspanspan-idsystemrequirementsspanspan-idsystemrequirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>系统要求


内核调试通过以太网 Nic 需要某些低级别平台的支持。 Windows 需要两个 Nic 通过 PCI/PCIe 附加此调试解决方案。 在大多数情况下，只需插入这些受支持的 Nic 之一将允许功能强大的内核调试体验。 但是，可能有其中 BIOS 配置详细信息会影响 Windows 调试路径的情况。 应考虑以下一组平台要求：

-   系统固件应发现和配置 NIC 设备，使其资源不与任何其他设备，已进行 BIOS 配置冲突。
-   系统固件应放置在未标记为 prefetchable 地址 windows 下的 NIC 的资源。

## <a name="span-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>查找供应商 ID 和设备 ID


首先在目标计算机上找到的供应商 ID 和设备 ID 的网络适配器。

-   在目标计算机上打开设备管理器 (输入**devmgmt**在命令提示符窗口中)。
-   在设备管理器中，找到你想要用于调试的网络适配器。
-   右键单击网络适配器节点，然后选择**属性**。
-   在中**详细信息**选项卡上，在**属性**，选择**硬件 Id**。

也执行如下所示的供应商和设备 Id\_*VendorID*和 DEV\_*DeviceID*。 例如，如果您看到 PCI\\即使\_8086 & 开发\_104B，供应商 ID 是 8086，而设备 ID 是 104B。

## <a name="span-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>Vendor ID 8086, Intel Corporation


对于供应商 ID 8086，支持下列设备 Id:

1000 1001年 1004年 1008年 1009年 100C 100 D 100E 100F 1010年 1011年 1012年 1013年 1014年 1015年 1016年 1017年 1018年 1019年 101A 101 D 101E 1026年 1027年 1028年 1049年 104A 104B 104C 104 D 105E 105F 1060年 1075年 1076年 1077年 1078年 1079年 107A 107B 107C 107 D 107E 107F 108A 108B 108C 1096年 1098年 1099年 109A 10A4 10A5 10A7 10A910B5 10B9 10BA 10BB 10BC 10BD 10BF 10C 9 10CB 10CC 10 CD 10CE 10 个 D 3 10 个 D 5 10 个 D 6 10D 9 10DA 10E5 10E6 10E7 10E8 10EA 10EB 10EF 10F0 10F5 10F6 1501年 1502年 1503年 150A 150 C 150 D 150E 150F 1510年 1511年 1516年 1518年 1521年 1522年 1523年 1524年 1526年 294C
## <a name="span-idvendorid10ecrealteksemiconductorcorpspanspan-idvendorid10ecrealteksemiconductorcorpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>供应商 ID 10EC，Realtek 半导体 corp.


对于供应商 ID 10EC，支持下列设备 Id:

8136 8137 8167 8168 8169
## <a name="span-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>供应商 ID 14E4 Broadcom


对于供应商 ID 14E4，支持下列设备 Id:

1600 1601年 1639年 163A 163B 163C 1644年 1645年 1646年 1647年 1648年 164A 164 C 164D 1653年 1654年 1655年 1656年 1657年 1658年 1659年 165A 165B 165C 165 D 165E 165F 1668 1669年 166A 166B 166 D 166E 1672年 1673年 1674年 1676年 1677年 1678年 1679年 167A 167B 167 C 167 D 167F 1680年 1681年 1684年 1688年 1690年 1691年 1692年 1693年 1694年 1696年1698 1699 169A 169B 169 D 16A0 16A6 16A7 16A8 16AA 16AC 16B0 16B1 16B2 16B4 16B5 16B6 16C 6 16C 7 16DD 16F7 16FD 16FE 16FF 170 D 170E 170F
## <a name="span-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>供应商 ID 1969，Atheros 通信


由单独的模块，可从 Qualcomm 提供 Atheros 网络适配器的支持。 支持下列设备 Id。

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题



[KDNET 网络内核调试会自动设置](setting-up-a-network-debugging-connection-automatically.md)

[支持的网络内核调试在 Windows 8.1 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[支持的网络内核调试在 Windows 10 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

 

 






