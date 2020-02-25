---
title: Windows 8.1 中的网络内核调试支持的以太网 NIC
description: 当目标计算机运行 Windows 8.1 时，可以通过以太网网络电缆进行内核调试。 目标计算机必须具有支持的网络接口卡（NIC）或网络适配器。
ms.assetid: C608A406-C008-4075-B6BE-C14CFFC3A820
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 575e459e6720efecda8398bdec9b7bbe377704d2
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528966"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-81"></a>Windows 8.1 中的网络内核调试支持的以太网 NIC

当目标计算机运行 Windows 8.1 时，可以通过以太网网络电缆进行内核调试。 目标计算机必须具有支持的网络接口卡（NIC）或网络适配器。

在内核调试过程中，运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。 有关详细信息，请参阅[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

若要通过网络电缆进行内核调试，目标计算机必须具有支持的网络适配器。 当目标计算机运行 Windows 8.1 时，将支持此处列出的网络适配器进行内核调试。

**请注意**，在所选的 10 gigabit 网络适配器上进行内核调试  支持是 Windows 8.1 中的一项新功能。 在 Windows 8 中不支持通过 10 gb 网络适配器进行调试。 有关适用于内核调试的 Windows 8 支持的网络适配器列表，请参阅[windows 8 中的网络内核调试支持的以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)。

## <a name="span-idsystem_requirementsspanspan-idsystem_requirementsspanspan-idsystem_requirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>系统要求

通过以太网 Nic 进行内核调试需要某些低级别平台支持。 Windows 要求通过 PCI/PCIe 附加这些 Nic 才能实现此调试解决方案。 在大多数情况下，只需插入其中一个受支持的 Nic 即可实现可靠的内核调试体验。 但是，可能存在 BIOS 配置详细信息阻碍 Windows 调试路径的情况。 应考虑以下平台要求：

-  系统固件应发现并配置 NIC 设备，使其资源不与 BIOS 配置的任何其他设备冲突。

## <a name="span-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>查找供应商 ID 和设备 ID

首先查找目标计算机上的网络适配器的供应商 ID 和设备 ID。

-  在目标计算机上，打开设备管理器（在命令提示符窗口中输入**devmgmt.msc** ）。
-  在设备管理器中，找到要用于调试的网络适配器。
-  右键单击网络适配器节点，然后选择 "**属性**"。
-  在 "**详细信息**" 选项卡的 "**属性**" 下，选择 "**硬件 id**"。

供应商和设备 Id 显示为即使\_*VendorID*和 DEV\_*DeviceID*。 例如，如果你看到 PCI\\即使\_8086 & 开发\_104B，则供应商 ID 为8086，并且设备 ID 为104B。

## <a name="span-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>供应商 ID 8086，Intel Corporation

对于供应商 ID 8086，支持以下设备 Id：

0438 043A 043C 0440 1000 1001 1004 1008 1009 100C 100D 100E 100F 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101D 101E 1026 1027 1028 1049 104A 104B 104C 104D 105E 105F 1060 1075 1076 1077 1078 1079 107A 107B 107C 107D 107E 107F 108A 108B 108C 1096 1098 1099 109A10A4 10A5 10A7 10A9 10B5 10B9 10BA 10BB 10BC 10BD 10BF 10C0 10C2 10C3 10C4 10C5 10C6 10C7 10C8 10C9 10CB 10CC 10CD 10CE 10D3 10D5 10D6 10D9 10DA 10DB 10DD 10DE 10DF 10E1 10E5 10E6 10E7 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10F5 10F6 10F7 10F8 10F9 10FA 10FB 10FC 1501 15021503 1507 150A 150B 150C 150D 150E 150F 1510 1511 1514 1516 1517 1518 151C 1521 1522 1523 1524 1525 1526 1527 1528 1529 1533 1534 1535 1536 1537 1538 1539 152A 153A 153B 154A 154D 155A 157B 1546 157C 1557 1558 1559 1F40 1F41 1F45 294C
## <a name="span-idvendor_id_10ec__realtek_semiconductor_corpspanspan-idvendor_id_10ec__realtek_semiconductor_corpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>供应商 ID 10EC，Realtek 半导体公司。


对于供应商 ID 10EC，支持以下设备 Id：

8136 8137 8167 8168 8169
## <a name="span-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>供应商 ID 14E4，Broadcom


对于供应商 ID 14E4，支持以下设备 Id：

1600 1601 1639 163A 163B 163C 1644 1645 1646 1647 1648 164A 164C 164D 1653 1654 1655 1656 1657 1658 1659 165A 165B 165C 165D 165E 165F 1668 1669 166A 166B 166D 166E 1672 1673 1674 1676 1677 1678 1679 167A 167B 167C 167D 167F 1680 1681 1684 1688 1690 1691 1692 1693 1694 16961698 1699 169A 169B 169D 16A0 16A6 16A7 16A8 16AA 16AC 16B0 16B1 16B2 16B4 16B5 16B6 16C6 16C7 16DD 16F7 16FD 16FE 16FF 170D 170E 170F
## <a name="span-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>供应商 ID 1969，Atheros 通信


对于供应商 ID 1969，支持以下设备 Id：

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idvendor_id_19a2__serverengines__emulex_spanspan-idvendor_id_19a2__serverengines__emulex_spanspan-idvendor_id_19a2__serverengines__emulex_spanvendor-id-19a2-serverengines-emulex"></a><span id="Vendor_ID_19A2__ServerEngines__Emulex_"></span><span id="vendor_id_19a2__serverengines__emulex_"></span><span id="VENDOR_ID_19A2__SERVERENGINES__EMULEX_"></span>供应商 ID 19A2，ServerEngines （Emulex）


对于供应商 ID 19A2，支持以下设备 Id：

0211 0215 0221 0700 0710
## <a name="span-idvendor_id_10df__emulex_corporationspanspan-idvendor_id_10df__emulex_corporationspanspan-idvendor_id_10df__emulex_corporationspanvendor-id-10df-emulex-corporation"></a><span id="Vendor_ID_10DF__Emulex_Corporation"></span><span id="vendor_id_10df__emulex_corporation"></span><span id="VENDOR_ID_10DF__EMULEX_CORPORATION"></span>供应商 ID 10DF，Emulex Corporation


对于供应商 ID 10DF，支持以下设备 Id：

0720 E220
## <a name="span-idvendor_id_15b3__mellanox_technologyspanspan-idvendor_id_15b3__mellanox_technologyspanspan-idvendor_id_15b3__mellanox_technologyspanvendor-id-15b3-mellanox-technology"></a><span id="Vendor_ID_15B3__Mellanox_Technology"></span><span id="vendor_id_15b3__mellanox_technology"></span><span id="VENDOR_ID_15B3__MELLANOX_TECHNOLOGY"></span>供应商 ID 15B3，Mellanox 技术


对于供应商 ID 15B3，支持以下设备 Id：

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100A 100B 100C 100D 100E 1010 6340 6341 100F 634A 634B 673C 6354 6368 6369 6372 6732 6733 673D 675A 6746 6750 6751 676E 6764 6765 6778

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题



[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)

[Windows 8 中用于网络内核调试的受支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 

 






