---
title: 安装蓝牙设备
description: 安装蓝牙设备
keywords:
- 蓝牙 WDK，蓝牙驱动程序安装
- 客户端配置文件驱动程序 WDK 蓝牙
- 服务器端配置文件驱动程序 WDK 蓝牙
- INF 文件 WDK 蓝牙
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 54f4ffcae404e4f944661bdff699fc7ce7ed0030
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798529"
---
# <a name="installing-a-bluetooth-device"></a>安装蓝牙设备

> [!IMPORTANT]
> 本主题面向程序员。 如果你是遇到蓝牙设备安装问题的客户，请参阅 [在 Windows 中配对蓝牙设备](https://support.microsoft.com/help/15290/windows-connect-bluetooth-device)

蓝牙配置文件驱动程序有两种安装类型：

- 远程设备的 **客户端安装**，远程设备在该远程设备上公布其服务并且计算机连接到它。 示例包括：鼠标设备、键盘和打印机。

- **服务器端安装** ，其中计算机公布服务和远程设备可以连接到计算机以使用这些服务。 例如，供应商可能会创作服务器端安装，以使 PDA 能够打印到连接到计算机的打印机。

这两种安装类型需要不同的安装过程。

## <a name="installing-a-client-side-profile-driver"></a>安装客户端配置文件驱动程序

如果用户想要使用启用 Bluetooth 的设备，则会将设备置于计算机范围内，并使用客户端配置文件驱动程序的以下安装顺序启动从计算机到远程设备的连接。

1. 在 **控制面板** 中启动蓝牙设备，查找计算机范围内的所有设备。

2. 选择要配对的设备。

3. 将 (或绑定与本地无线电) 设备配对。 这不一定涉及 PIN 交换。

4. 本地收音机发出一个 SDP 查询，用于识别远程设备上支持的服务。

5. " **发现新硬件" 向导** 在本地硬盘驱动器上搜索合适的驱动程序，并在 Windows 更新上搜索/或。

6. 如果 **发现的新硬件向导** 找不到设备的适当驱动程序，系统会提示用户插入配置文件驱动程序安装媒体，其中包含配置文件驱动程序的设备安装信息文件 (INF 文件) 。

## <a name="installing-a-server-side-profile-driver"></a>安装服务器端配置文件驱动程序

蓝牙驱动程序堆栈支持蓝牙 SIG 定义的服务 Guid，以及自定义 Guid (即，不是由蓝牙 SIG) 定义的 Guid。

> [!NOTE]
> Microsoft Windows SDK 提供的 **Guidgen.exe** 工具可用于创建自定义 guid。

必须编写用户模式安装应用程序才能公开远程蓝牙设备可以使用的计算机功能。

安装应用程序必须与蓝牙驱动程序堆栈进行通信，以便为要公开的功能创建服务 GUID。 供应商在应用程序和其设备安装 INF 文件中指定服务 GUID。

安装应用程序必须调用用户模式 API [BluetoothSetLocalServiceInfo](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothsetlocalserviceinfo)。 在应用程序可以调用此 API 之前，应用程序必须具有 "SE \_ 加载 \_ 驱动程序 \_ 名称" 安全权限。 下面的代码示例演示如何获取此特权。 **请注意** ，该示例不演示错误处理。

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

## <a name="profile-driver-inf-file"></a>配置文件驱动程序 INF 文件

配置文件驱动程序的 INF 文件包含有关用于客户端安装的蓝牙设备的信息。 对于服务器端安装，INF 文件指定了与安装应用程序创建的服务 GUID 相对应的设备 ID。 所有蓝牙设备均为 **蓝牙** 类的成员。 蓝牙类安装程序 (*Bthci.dll*) 可帮助安装配置文件驱动程序。

有关创建和分发 INF 文件和安装驱动程序的详细信息，请参阅 [创建 Inf 文件](../install/overview-of-inf-files.md) 和 [inf 文件部分和指令](../install/index.md)。

### <a name="plug-and-play-ids"></a>即插即用 Id

蓝牙驱动程序堆栈根据以下模板生成硬件 Id：

- BTHENUM \\ { *ServiceGUID*} \_ VID& *nnnnnnnn*

- BTHENUM \\ { *ServiceGUID*} \_ VID& *nnnnnnnn* \_ PID& *nnnn*

- BTHENUM \\ { *ServiceGUID*} \_ LOCALMFG& *nnnn*

蓝牙驱动程序堆栈根据以下模板生成兼容的 Id：

- BTHENUM \\ { *ServiceGUID*}

*ServiceGUID* 是扩展为128位 guid 的16位 guid，由蓝牙规范定义。 例如，{00001124-0000-1000-8000-00805F9B34FB} 对应于一个 HID 设备。

- VID 后面的8位 *&* 对应于供应商 ID 代码。

- PID 后面的4位数 *&* 对应于产品 ID 代码。

- LOCALMFG 后面的4位数 *&* 与本地蓝牙无线电的制造商相对应。

- VID/PID 和 LOCALMFG 标记彼此独立。

最常见的设备 ID 是 *ServiceGUID* 本身。 例如：

BTHENUM \\ {00001124-0000-1000-8000-00805F9B34FB}

通过使用远程设备和 INF 文件中的即插即用 Id，可以限制蓝牙驱动程序堆栈加载配置文件驱动程序和软件，以便仅在远程设备的特定版本上运行。 **请注意** ，仅当设备发布了堆栈可以使用 SDP 检测即插即用 ID 时，蓝牙驱动程序堆栈才生成 VID/PID 对。 例如：

BTHENUM \\ {00001124-0000-1000-8000-00805F9B34FB} \_ VID& *nnnnnnnn* \_ PID& *nnnn*

可以通过在 INF 文件中的设备 ID 中指定 LOCALMFG 标记，将蓝牙驱动程序堆栈限制为仅加载配置文件驱动程序和软件以便在特定本地蓝牙收音机上运行。 例如：

BTHENUM \\ {00001124-0000-1000-8000-00805F9B34FB} \_ LOCALMFG& *nnnn*
