---
title: 安装 Bluetooth 的设备
description: 安装 Bluetooth 的设备
ms.assetid: 2bf2b2df-260c-42a5-9ee9-6db91f304036
keywords:
- 蓝牙 WDK 安装
- 客户端配置文件驱动程序 WDK 蓝牙
- 服务器端配置文件驱动程序 WDK 蓝牙
- INF 文件 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 212adebec6cd3e04f98c905d70da82bb39109cbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534585"
---
# <a name="installing-a-bluetooth-device"></a>安装 Bluetooth 的设备


蓝牙配置文件驱动程序的两种安装类型

1.  客户端安装

2.  服务器端的安装

客户端安装适用于远程设备的远程设备播发其服务并在计算机连接到它。 示例包括： 鼠标设备、 键盘和打印机。

服务器端的安装是计算机播发服务和远程设备可以连接到计算机以使用这些服务。 例如，供应商可以创建服务器端的安装，以启用 PDA 打印到打印机连接到计算机。

这两种安装类型需要不同的安装过程。

### <a name="span-idinstallingaclientsideprofiledriverspanspan-idinstallingaclientsideprofiledriverspaninstalling-a-client-side-profile-driver"></a><span id="installing_a_client_side_profile_driver"></span><span id="INSTALLING_A_CLIENT_SIDE_PROFILE_DRIVER"></span>**安装客户端配置文件驱动程序**

当用户想要使用已启用蓝牙的设备时，用户应将设备的计算机范围内，启动从计算机到远程设备的连接。 下面是客户端配置文件驱动程序安装的安装顺序。

**若要安装客户端配置文件驱动程序**

1.  启动蓝牙设备中**控制面板**查找的计算机范围内的所有设备。

2.  选择要与之匹配的设备。

3.  配对 （或绑定） 与本地无线电收发器设备。 这可能会或可能不涉及 PIN exchange。

4.  本地无线电收发器发出一个 SDP 查询，以确定在远程设备上受支持的服务。

5.  **发现新硬件向导**搜索合适的驱动程序在本地硬盘驱动器上，和/或 Windows 更新。

6.  如果**发现新硬件向导**不到相应的驱动程序对于设备，它会提示用户插入包含配置文件驱动程序的设备安装程序信息文件 （INF 文件） 的配置文件驱动程序安装介质。

### <a name="span-idinstallingaserversideprofiledriverspanspan-idinstallingaserversideprofiledriverspaninstalling-a-server-side-profile-driver"></a><span id="installing_a_server_side_profile_driver"></span><span id="INSTALLING_A_SERVER_SIDE_PROFILE_DRIVER"></span>**安装服务器端配置文件驱动程序**

蓝牙驱动程序堆栈支持服务 Guid 由蓝牙 SIG，定义和自定义 Guid (即，未定义的蓝牙 SIG 的 Guid)。

**请注意**  可以使用*Guidgen.exe*工具，它提供与 Microsoft Windows SDK 创建自定义 Guid。

 

若要公开远程蓝牙设备可以使用的计算机功能，必须编写用户模式下安装应用程序。

安装应用程序必须与要创建服务的功能要公开的 GUID 的蓝牙驱动程序堆栈进行通信。 在应用程序并在其设备安装 INF 文件中，供应商指定的服务 GUID。

安装应用程序必须调用用户模式 API **BluetoothSetLocalServiceInfo**。 但是，应用程序可以调用此 API 之前，应用程序必须具有 SE\_负载\_驱动程序\_名称安全特权。 下面的代码示例演示如何获取此权限。 请注意，该示例不演示错误处理。

```cpp
HANDLE procToken;
LUID luid;
TOKEN_PRIVILEGES tp;

OpenProcessToken(GetCurrentProcess(), TOKEN_ADJUST_PRIVILEGES | TOKEN_QUERY, &procToken);

LookupPrivilegeValue(NULL, SE_LOAD_DRIVER_NAME, &luid);

Tp.PrivilegeCount = 1;
Tp.privileges[0].Luid = luid;
Tp.Privileges[0].Attributes = SE_PRIVILEGE_ENABLED;

AdjustTokenPrivileges(procToken, FALSE, &tp, sizeof(TOKEN_PRIVILEGES), (PTOKEN_PRIVILEGES) NULL, (PDWORD)NULL)
```

### <a name="span-idprofiledriverinffilespanspan-idprofiledriverinffilespanprofile-driver-inf-file"></a><span id="profile_driver_inf_file"></span><span id="PROFILE_DRIVER_INF_FILE"></span>**配置文件驱动程序 INF 文件**

配置文件驱动程序的 INF 文件包含有关客户端安装的蓝牙设备的信息。 对于服务器端的安装，INF 文件指定对应于服务安装应用程序创建的 GUID 的设备 ID。 所有蓝牙设备都属于**蓝牙**类。 蓝牙类安装程序 ( *Bthci.dll*) 可帮助您进行安装配置文件驱动程序。

有关创建和分发 INF 文件和安装驱动程序的详细信息，请参阅[创建一个 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff549520)并[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

### <a name="span-idplugandplayidsspanspan-idplugandplayidsspanplug-and-play-ids"></a><span id="plug_and_play_ids"></span><span id="PLUG_AND_PLAY_IDS"></span>**Plug and Play Id**

蓝牙驱动程序堆栈会根据以下模板生成的硬件 Id:

-   BTHENUM\\{ *ServiceGUID*}\_VID & *nnnnnnnn*

-   BTHENUM\\{ *ServiceGUID*}\_VID & *nnnnnnnn*\_PID & *nnnn*

-   BTHENUM\\{ *ServiceGUID*}\_LOCALMFG & *nnnn*

蓝牙驱动程序堆栈生成兼容 Id 根据以下模板：

-   BTHENUM\\{ *ServiceGUID*}

*ServiceGUID* 16 位 GUID 展开为 128 位 GUID，因为蓝牙规范所定义。 例如，{00001124-0000-1000-8000-00805F9B34FB} 对应于 HID 设备。

8 跟随的数字*VID &* 对应的供应商 ID 代码。

以下的 4 位数*PID （& a)* 对应于的产品 ID 代码。

以下的 4 位数*LOCALMFG &* 对应于本地的 Bluetooth 无线电收发器制造商。

VID/PID 和 LOCALMFG 标记是相互独立。

ID 是最通用设备*ServiceGUID*本身。 例如：

BTHENUM\\{00001124-0000-1000-8000-00805F9B34FB}

你可以限制蓝牙驱动程序堆栈，以加载你的配置文件驱动程序和软件仅在特定版本的远程设备上运行使用插在远程设备和 INF 文件中的 Id。 请注意蓝牙驱动程序堆栈生成 VID/PID 对，仅当设备发布堆栈可以检测到使用 SDP 插 ID。 例如：

BTHENUM\\{00001124-0000-1000-8000-00805F9B34FB}\_VID & *nnnnnnnn*\_PID & *nnnn*

你可以限制要加载配置文件驱动程序和软件，通过在您的 INF 文件中的设备 ID 指定 LOCALMFG 标记仅在特定的本地蓝牙无线上运行的蓝牙驱动程序堆栈。 例如：

BTHENUM\\{00001124-0000-1000-8000-00805F9B34FB}\_LOCALMFG & *nnnn*

 

 





