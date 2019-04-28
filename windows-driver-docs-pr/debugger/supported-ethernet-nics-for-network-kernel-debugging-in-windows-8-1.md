---
title: Windows 8.1 中的网络内核调试支持的以太网 NIC
description: 你可以执行在目标计算机正在运行 Windows 8.1 时内核调试通过以太网网络电缆。 目标计算机必须具有支持的网络接口卡 (NIC) 或网络适配器。
ms.assetid: C608A406-C008-4075-B6BE-C14CFFC3A820
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89b9ae9f1ca4bf7047251af014b19807671f5453
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335494"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-81"></a>Windows 8.1 中的网络内核调试支持的以太网 NIC


你可以执行在目标计算机正在运行 Windows 8.1 时内核调试通过以太网网络电缆。 目标计算机必须具有支持的网络接口卡 (NIC) 或网络适配器。

在内核调试，期间调用运行调试器的计算机*主机计算机*，和正在调试的计算机称为*目标计算机*。 若要执行操作[内核调试通过网络电缆](setting-up-a-network-debugging-connection.md)，目标计算机必须具有支持的网络适配器。 当目标计算机正在运行 Windows 8.1 时，此处列出的网络适配器支持内核调试。

**请注意**  支持针对内核调试超过选定 10 千兆位网络适配器是在 Windows 8.1 中的新功能。 超过 10 千兆位网络适配器不支持调试在 Windows 8 中。 有关支持的 Windows 8 的内核调试网络适配器的列表，请参阅[用于在 Windows 8 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)。

 

## <a name="span-idsystemrequirementsspanspan-idsystemrequirementsspanspan-idsystemrequirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>系统要求


内核调试通过以太网 Nic 需要某些低级别平台的支持。 Windows 需要两个 Nic 通过 PCI/PCIe 附加此调试解决方案。 在大多数情况下，只需插入这些受支持的 Nic 之一将允许功能强大的内核调试体验。 但是，可能有其中 BIOS 配置详细信息会影响 Windows 调试路径的情况。 应考虑以下平台要求：

-   系统固件应发现和配置 NIC 设备，使其资源不与任何其他设备，已进行 BIOS 配置冲突。

## <a name="span-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>查找供应商 ID 和设备 ID


首先在目标计算机上找到的供应商 ID 和设备 ID 的网络适配器。

-   在目标计算机上打开设备管理器 (输入**devmgmt**在命令提示符窗口中)。
-   在设备管理器中，找到你想要用于调试的网络适配器。
-   右键单击网络适配器节点，然后选择**属性**。
-   在中**详细信息**选项卡上，在**属性**，选择**硬件 Id**。

也执行如下所示的供应商和设备 Id\_*VendorID*和 DEV\_*DeviceID*。 例如，如果您看到 PCI\\即使\_8086 & 开发\_104B，供应商 ID 是 8086，而设备 ID 是 104B。

## <a name="span-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>Vendor ID 8086, Intel Corporation


对于供应商 ID 8086，支持下列设备 Id:

0438 043A 043C 0440年 1000年 1001年 1004年 1008年 1009年 100C 100 D 100E 100F 1010年 1011年 1012年 1013年 1014年 1015年 1016年 1017年 1018年 1019年 101A 101 D 101E 1026年 1027年 1028年 1049年 104A 104B 104C 104 D 105E 105F 1060年 1075年 1076年 1077年 1078年 1079年 107A 107B 107 C 107 D 107E 107F 108A 108B 108C 1096年 1098年 1099年 109A10A4 10A5 10A7 10A9 10B5 10B9 10BA 10BB 10BC 10BD 10BF 10C 0 10C 2 10C 3 10C 4 10C 5 10C 6 10C 7 10C 8 10C 9 10CB 10CC 10 CD 10CE 10 个 D 3 10 个 D 5 10 个 D 6 10D 9 10DA 10DB 10DD 10DE 10DF 10E1 10E5 10E6 10E7 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10F5 10F6 10F7 10F8 10F9 10FA 10FB 10 FC 1501 15021503 1507 150A 150B 150 C 150 D 150E 150F 1510年 1511年 1514年 1516年 1517年 1518年 151C 1521年 1522年 1523年 1524年 1525年 1526年 1527年 1528年 1529年 152A 1533年 1534年 1535年 1536年 1537年 1538年 1539年 153A 153B 1546年 154A 154D 1557年 1558年 1559年 155A 1560年 157B 157 C 1F40 1F41 1F45 294 C
## <a name="span-idvendorid10ecrealteksemiconductorcorpspanspan-idvendorid10ecrealteksemiconductorcorpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>供应商 ID 10EC，Realtek 半导体 corp.


对于供应商 ID 10EC，支持下列设备 Id:

8136 8137 8167 8168 8169
## <a name="span-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>供应商 ID 14E4 Broadcom


对于供应商 ID 14E4，支持下列设备 Id:

1600 1601年 1639年 163A 163B 163C 1644年 1645年 1646年 1647年 1648年 164A 164 C 164D 1653年 1654年 1655年 1656年 1657年 1658年 1659年 165A 165B 165C 165 D 165E 165F 1668 1669年 166A 166B 166 D 166E 1672年 1673年 1674年 1676年 1677年 1678年 1679年 167A 167B 167 C 167 D 167F 1680年 1681年 1684年 1688年 1690年 1691年 1692年 1693年 1694年 1696年1698 1699 169A 169B 169 D 16A0 16A6 16A7 16A8 16AA 16AC 16B0 16B1 16B2 16B4 16B5 16B6 16C 6 16C 7 16DD 16F7 16FD 16FE 16FF 170 D 170E 170F
## <a name="span-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>供应商 ID 1969，Atheros 通信


对于供应商 ID 1969，支持下列设备 Id:

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idvendorid19a2serverenginesemulexspanspan-idvendorid19a2serverenginesemulexspanspan-idvendorid19a2serverenginesemulexspanvendor-id-19a2-serverengines-emulex"></a><span id="Vendor_ID_19A2__ServerEngines__Emulex_"></span><span id="vendor_id_19a2__serverengines__emulex_"></span><span id="VENDOR_ID_19A2__SERVERENGINES__EMULEX_"></span>供应商 ID 19A2，ServerEngines (Emulex)


对于供应商 ID 19A2，支持下列设备 Id:

0211 0215 0221 0700 0710
## <a name="span-idvendorid10dfemulexcorporationspanspan-idvendorid10dfemulexcorporationspanspan-idvendorid10dfemulexcorporationspanvendor-id-10df-emulex-corporation"></a><span id="Vendor_ID_10DF__Emulex_Corporation"></span><span id="vendor_id_10df__emulex_corporation"></span><span id="VENDOR_ID_10DF__EMULEX_CORPORATION"></span>供应商 ID 10DF，Emulex Corporation


对于供应商 ID 10DF，支持下列设备 Id:

0720 E220
## <a name="span-idvendorid15b3mellanoxtechnologyspanspan-idvendorid15b3mellanoxtechnologyspanspan-idvendorid15b3mellanoxtechnologyspanvendor-id-15b3-mellanox-technology"></a><span id="Vendor_ID_15B3__Mellanox_Technology"></span><span id="vendor_id_15b3__mellanox_technology"></span><span id="VENDOR_ID_15B3__MELLANOX_TECHNOLOGY"></span>供应商 ID 15B3，Mellanox 技术


对于供应商 ID 15B3，支持下列设备 Id:

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100A 100B 100C 100D 100E 100F 1010 6340 6341 634A 634B 6354 6368 6369 6372 6732 6733 673C 673D 6746 6750 6751 675A 6764 6765 676E 6778

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题



[KDNET 网络内核调试会自动设置](setting-up-a-network-debugging-connection-automatically.md)

[支持的网络内核调试 Windows 8 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 

 






