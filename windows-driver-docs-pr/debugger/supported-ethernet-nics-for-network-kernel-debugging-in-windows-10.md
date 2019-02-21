---
title: 支持的网络内核调试在 Windows 10 中的以太网 Nic
description: 您可以执行操作时目标计算机运行的 Windows 内核调试通过以太网网络电缆。 目标计算机必须具有支持的网络接口卡 (NIC) 或网络适配器。
ms.assetid: F98A7ACE-DD04-423C-A438-89E21363C693
ms.date: 12/04/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4653c71d6a736abf7f36a2d713384d0d6478666e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540610"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-10"></a>支持的网络内核调试在 Windows 10 中的以太网 Nic

您可以执行操作时目标计算机运行的 Windows 内核调试通过以太网网络电缆。 目标计算机必须具有支持的网络接口卡 (NIC) 或网络适配器。

在内核调试，期间调用运行调试器的计算机*主机计算机*，和正在调试的计算机称为*目标计算机*。 若要执行操作[内核调试通过网络电缆](setting-up-a-network-debugging-connection.md)，目标计算机必须具有支持的网络适配器。 当目标计算机正在运行 Windows 时，此处列出的网络适配器支持内核调试。

**版本信息**  

支持的适配器的列表是针对以下版本的 Windows

-   Windows 10，版本 1809
-   Windows Server 2019


**适配器支持 Windows 的早期版本**  

若要确定对于任何特定版本的 Windows 支持的 Nic 的一组，请检查`VerifiedNicList.xml`WDK 随附了该特定版本的 Windows 安装的调试器目录中的文件。 适用于 64 位 Windows，默认情况下，它将安装在此目录中：

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\VerifiedNicList.xml`

检查在特定版本的 WDK 中随附 VerifiedNicList.xml，需要，因为其他硬件支持添加到新版本的 Windows 的早期版本中不存在。  因此必须检查该特定版本的 VerifiedNicLIst.xml 文件。


## <a name="span-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>查找供应商 ID 和设备 ID

首先在目标计算机上找到的供应商 ID 和设备 ID 的网络适配器。

-   在目标计算机上打开设备管理器 (输入**devmgmt**在命令提示符窗口中)。
-   在设备管理器中，找到你想要用于调试的网络适配器。
-   右键单击网络适配器节点，然后选择**属性**。
-   在中**详细信息**选项卡上，在**属性**，选择**硬件 Id**。

也执行如下所示的供应商和设备 Id\_*VendorID*和 DEV\_*DeviceID*。 例如，如果您看到 PCI\\即使\_8086 & 开发\_104B，供应商 ID 是 8086，而设备 ID 是 104B。

## <a name="span-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>Vendor ID 8086, Intel Corporation


对于供应商 ID 8086，支持下列设备 Id:

0001 0008 000 C 000D 0438年 043A 043C 0440年 0470年 1000年 1001年 1004年 1008年 1009年 100C 100 D 100E 100F 1010年 1011年 1012年 1013年 1014年 1015年 1016年 1017年 1018年 1019年 101A 101 D 101E 1026年 1027年 1028年 1049年 104A 104B 104C 104 D 105E 105F 1060年 1071年 1075年 1076年 1077年 1078年 1079年 107A 107B 107 C 107 D 107E 107F 108A108B 108C 1096年 1098年 1099年 109A 10A4 10A5 10A7 10A9 10B5 10B9 10BA 10BB 10BC 10BD 10BF 10C 0 10C 2 10C 3 10C 4 10C 5 10C 6 10C 7 10C 8 10C 9 10CB 10CC 10 CD 10CE 10 个 D 3 10 个 D 5 10 个 D 6 10D 9 10DA 10DB 10DD 10DE 10DF 10E1 10E5 10E6 10E7 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10F5 10F6 10F7 10F810F9 10FB 10 FC 11A9 1501年 1502年 1503年 1507年 150A 150B 150 C 150 D 150E 150F 1510年 1511年 1514年 1516年 1517年 1518年 151C 1521年 1522年 1523年 1524年 1525年 1526年 1527年 1528年 1529年 152A 1533年 1534年 1535年 1536年 1537年 1538年 1539年 153A 153B 1546年 154A 154D 1557年 1558年 1559年 155A 1560 1563年 156F 1570年 157B 157 C 15A0 15A115A2 15A3 15AA 15AB 15AC 15AD 15AE 15B7 15B8 17 D 0 1F40 1F41 1F45 1F63 1F72 211B 2159年 294 C 8976

## <a name="span-idvendorid10ecrealteksemiconductorcorpspanspan-idvendorid10ecrealteksemiconductorcorpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>供应商 ID 10EC，Realtek 半导体 corp.


对于供应商 ID 10EC，支持下列设备 Id:

8136 8137 8166 8167 8168 8169

## <a name="span-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>供应商 ID 14E4 Broadcom


对于供应商 ID 14E4，支持下列设备 Id:

1600 1601年 1639年 163A 163B 163C 163D 163E 1641年 1642年 1643年 1644年 1645年 1646年 1647年 1648年 164A 164C 164 D 164E 164F 1650年 1653年 1654年 1655年 1656年 1657年 1659年 165A 165B 165C 165 D 165E 165F 1662年 1663年 1665年 1668年 1669年 166A 166B 166 D 166E 1672年 1673年 1674年 1676年 1677年 1678年 1679年 167A 167B 167 C 167 D 167F168A 168 D 168E 1680年 1681年 1682年 1683年 1684年 1686年 1687年 1688年 1690年 1691年 1692年 1693年 1694年 1696年 1698年 1699年 169A 169B 169 D 16A0 16A1 16A2 16A4 16A5 16A6 16A7 16A8 16AA 16AC 16AE 16B0 16B1 16B2 16B3 16B4 16B5 16B6 16B7 16C 6 16C 7 16DD 16F7 16FD 16FE 16FF 170 D 170E 170F

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

1000 1001年 1002年 1003年 1004年 1005年 1006年 1007年 1008年 1009年 100A 100B 100 C 100 D 100E 100F 1010年 1013年 1015年 1017年 1019年 101B 101 D 101F 1021年 1023年 1025年 1027年 1029年 102B 102F 6340 6341 634A 634B 6354 6368 6369 6372 6732 6733 673C 673D 6746 6750 6751 675A 6764 6765 676E 6778

## <a name="span-idvendorid1137ciscosystemsincspanspan-idvendorid1137ciscosystemsincspanspan-idvendorid1137ciscosystemsincspanvendor-id-1137-cisco-systems-inc"></a><span id="Vendor_ID_1137__Cisco_Systems_Inc"></span><span id="vendor_id_1137__cisco_systems_inc"></span><span id="VENDOR_ID_1137__CISCO_SYSTEMS_INC"></span>供应商 ID 1137，Cisco Systems Inc


对于供应商 ID 1137，支持下列设备 Id:

0043

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[设置通过网络电缆在 Visual Studio 中的内核模式调试](setting-up-a-network-debugging-connection-in-visual-studio.md)

[KDNET 网络内核调试会自动设置](setting-up-a-network-debugging-connection-automatically.md)

[KDNET 网络内核调试手动设置](setting-up-a-network-debugging-connection.md)

[支持的网络内核调试 Windows 8 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

[支持的网络内核调试在 Windows 8.1 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

 

 






