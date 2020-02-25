---
title: Windows 8 中的网络内核调试支持的以太网 NIC
description: 当目标计算机运行 Windows 8 时，可以通过以太网网络电缆进行内核调试。 目标计算机必须具有支持的网络接口卡（NIC）或网络适配器。
ms.assetid: 92FEEBAF-9978-4BDE-BB4F-81454D84A7E7
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 07b9e6ec4ba7b12a3cc2681861dd204d290cb88b
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528951"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-8"></a>Windows 8 中的网络内核调试支持的以太网 NIC

当目标计算机运行 Windows 8 时，可以通过以太网网络电缆进行内核调试。 目标计算机必须具有支持的网络接口卡（NIC）或网络适配器。

在内核调试过程中，运行调试器的计算机称为*主机计算机*，被调试的计算机称为*目标计算机*。 有关详细信息，请参阅[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

若要通过网络电缆进行内核调试，目标计算机必须具有支持的网络适配器。 当目标计算机运行 Windows 8 时，此处列出的网络适配器支持内核调试。

**请注意**  Windows 8.1 用于内核调试的网络适配器列表，请参阅[Windows 8.1 中的网络内核调试支持的以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)。

## <a name="span-idsystem_requirementsspanspan-idsystem_requirementsspanspan-idsystem_requirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>系统要求

通过以太网 Nic 进行内核调试需要某些低级别平台支持。 Windows 要求通过 PCI/PCIe 附加这些 Nic 才能实现此调试解决方案。 在大多数情况下，只需插入其中一个受支持的 Nic 即可实现可靠的内核调试体验。 但是，可能存在 BIOS 配置详细信息阻碍 Windows 调试路径的情况。 应考虑以下平台要求：

- 系统固件应发现并配置 NIC 设备，使其资源不与 BIOS 配置的任何其他设备冲突。
- 系统固件应将 NIC 的资源置于未标记为 prefetchable 的地址窗口下。

## <a name="span-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>查找供应商 ID 和设备 ID

首先查找目标计算机上的网络适配器的供应商 ID 和设备 ID。

-  在目标计算机上，打开设备管理器（在命令提示符窗口中输入**devmgmt.msc** ）。
-  在设备管理器中，找到要用于调试的网络适配器。
-  右键单击网络适配器节点，然后选择 "**属性**"。
-  在 "**详细信息**" 选项卡的 "**属性**" 下，选择 "**硬件 id**"。

供应商和设备 Id 显示为即使\_*VendorID*和 DEV\_*DeviceID*。 例如，如果你看到 PCI\\即使\_8086 & 开发\_104B，则供应商 ID 为8086，并且设备 ID 为104B。

## <a name="span-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>供应商 ID 8086，Intel Corporation

对于供应商 ID 8086，支持以下设备 Id：

1000 1001 1004 1008 1009 100C 100D 100E 100F 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101D 101E 1026 1027 1028 1049 104A 104B 104C 104D 105E 105F 1060 1075 1076 1077 1078 1079 107A 107B 107C 107D 107E 107F 108A 108B 108C 1096 1098 1099 109A 10A4 10A5 10A7 10A910B5 10B9 10BA 10BB 10BC 10BD 10BF 10C9 10CB 10CC 10CD 10CE 10D3 10D5 10D6 10D9 10DA 10E5 10E6 10E7 10E8 10EA 10EB 10EF 10F0 10F5 10F6 1501 1502 1503 150A 150C 150D 150E 150F 1510 1511 1516 1518 1521 1522 1523 1524 1526 294C
## <a name="span-idvendor_id_10ec__realtek_semiconductor_corpspanspan-idvendor_id_10ec__realtek_semiconductor_corpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>供应商 ID 10EC，Realtek 半导体公司。


对于供应商 ID 10EC，支持以下设备 Id：

8136 8137 8167 8168 8169
## <a name="span-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>供应商 ID 14E4，Broadcom


对于供应商 ID 14E4，支持以下设备 Id：

1600 1601 1639 163A 163B 163C 1644 1645 1646 1647 1648 164A 164C 164D 1653 1654 1655 1656 1657 1658 1659 165A 165B 165C 165D 165E 165F 1668 1669 166A 166B 166D 166E 1672 1673 1674 1676 1677 1678 1679 167A 167B 167C 167D 167F 1680 1681 1684 1688 1690 1691 1692 1693 1694 16961698 1699 169A 169B 169D 16A0 16A6 16A7 16A8 16AA 16AC 16B0 16B1 16B2 16B4 16B5 16B6 16C6 16C7 16DD 16F7 16FD 16FE 16FF 170D 170E 170F
## <a name="span-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>供应商 ID 1969，Atheros 通信


对 Atheros 网络适配器的支持由一个可从 Qualcomm 提供的单独模块提供。 支持这些设备 Id。

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题



[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)

[Windows 8.1 中用于网络内核调试的受支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[Windows 10 中的网络内核调试支持的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

 

 






