---
title: BCDEdit/hypervisorsettings
description: /Hypervisorsettings 命令将设置或显示系统的虚拟机监控程序调试器设置。
ms.assetid: e86afc56-0304-4afe-9de5-980e5c83bf4f
ms.date: 10/01/2020
keywords:
- BCDEdit/hypervisorsettings 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /hypervisorsettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c610374ec8657c33cbdf6f2140d3fc45e1d3a526
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778968"
---
<a name="bcdedit-hypervisorsettings"></a>BCDEdit/hypervisorsettings
============

**/Hypervisorsettings**命令将设置或显示系统的虚拟机监控程序调试器设置。

若要设置单个虚拟机监控程序调试器设置，请使用 "bcdedit/set {hypervisorsettings} <type> <value>". 有关 set 命令的详细信息，请参阅 [BCDEdit/set](bcdedit--set.md)。

```syntax
bcdedit /hypervisorsettings [ <debugtype> [DEBUGPORT:<port>] [BAUDRATE:<baud>] [CHANNEL:<channel>] [HOSTIP:<ip>] [PORT:<port>] [BUSPARAMS:<Bus.Device.Function>] ]
```

*\<debugtype\>* -指定调试器的类型。 \<debugtype\> 可以是 NET、SERIAL 或1394中的一种，如下所述。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="network-debugging"></a>网络调试

\<debugtype\>*NET*  
指定用于调试的以太网网络连接。 使用此选项时，还必须通过指定主机调试程序的 IPv4 地址来设置 **HOSTIP** 选项。

**HOSTIP： * * \<ip\> * *仅当**hypervisordebugtype**为**Net**时才使用 IP 地址。 对于通过网络连接调试虚拟机监控程序，指定主机调试程序的 IPv4 地址。

**端口： * * \<port\> * *对于 "网络调试"，指定要在主机调试器上与之通信的端口。 必须是 49152 或以上。

**BUSPARAMS： * * \<Bus.Device.Function\> * *定义调试设备的 PCI 总线、设备和功能号。 例如，0.25.0 介绍了总线0上的调试设备，设备25，函数0。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

### <a name="network-debugging-example"></a>网络调试示例

以下命令将虚拟机监控程序调试器设置设置为使用在端口50000上的192.168.1.2 上的调试程序主机进行网络调试：

```console
C:\> bcdedit /hypervisorsettings NET HOSTIP:192.168.1.2 PORT:50000 BUSPARAMS:0.25.0
Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

使用返回的密钥来连接到目标。

可以使用 [BCDEdit/set](bcdedit--set.md) 命令修改这些网络调试设置。

**hypervisorhostip** *IP address*仅 hypervisordebugtype 为 Net 时使用。 ）若要通过网络连接调试虚拟机监控程序，请指定主机调试器的 IPv4 地址。 有关对 Hyper-V 进行调试的信息，请参阅[使用 Hyper-V 创建虚拟机](/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**hypervisorhostport** \[ *port* \]  
（仅 hypervisordebugtype 为 Net 时使用。 ）对于网络调试，请指定要在主机调试器上通信的端口。 必须是 49152 或以上。

**hypervisorbusparams** *Bus.Device.Function*  
定义调试设备的 PCI 总线、设备和功能号。 例如，0.25.0 介绍了总线0上的调试设备，设备25，函数0。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

**hypervisorusekey** *\<key\>* 仅当**hypervisordebugtype**为**Net**时才使用 (。 ) 用于网络调试指定用于对连接进行加密的密钥。   只允许 0-9 和 a-z 中的字符\[\]\[\]。

**hypervisordhcp** \[ **yes** | **no** \]  
控制虚拟机监控程序所使用的网络调试器使用 DHCP。 将此选项设置为不强制使用自动专用 IP 地址 (APIPA) 获取本地链接 IP 地址。

## <a name="serial-debugging"></a>串行调试 

\<debugtype\> *串行*  
指定用于调试的串行连接。 指定“串行”选项时，还可以设置 hypervisordebugport 和 hypervisorbaudrate 选项  。

**DEBUGPORT： * * \<port\> * *对于串行调试，指定要用作调试端口的串行端口。

**波特率： * * \<baud\> * *对于串行调试，指定用于调试的波特率。

``` syntax
bcdedit /set hypervisordebugtype serial
bcdedit /set hypervisordebugport 1
bcdedit /set hypervisorbaudrate 115200
bcdedit /set hypervisordebug on
bcdedit /set hypervisorlaunchtype auto
```

### <a name="serial-debugging-example"></a>串行调试示例

以下命令显示当前虚拟机监控程序设置。

```console
C:\>bcdedit /hypervisorsettings
isolatedcontext         Yes
hypervisordebugtype     Serial
hypervisordebugport     1
hypervisorbaudrate      115200
The operation completed successfully.
```

以下命令将虚拟机监控程序调试器设置设置为在115200波特通过 COM1 对 COM1 进行串行调试。

`bcdedit /hypervisorsettings SERIAL DEBUGPORT:1 BAUDRATE:115200`

## <a name="1394-debugging"></a>1394调试

> [!IMPORTANT]
> 1394 传输可用于 Windows 10 版本 1607 及更低版本。
> 它在 Windows 的更高版本中不可用。 应将项目转换为其他传输，例如使用以太网的 KDNET。

\<debugtype\> *1394*  
指定用于调试的 IEEE 1394 (FireWire) 连接。 使用此选项时，还应设置 *通道* 选项。

**频道： * * *<channel>*

对于1394调试，指定用于调试的1394通道。

应使用 [BCDEdit/set](bcdedit--set.md) 命令设置以下相关选项。

**hypervisorbusparams** *Bus.Device.Function*  
定义调试设备的 PCI 总线、设备和功能号。 例如，1.5.0 描述调试设备的总线 1、设备 5、功能 0。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

## <a name="comments"></a>注释

此命令不会启用或禁用任何特定操作系统加载器项的虚拟机监控程序调试器。 若要为特定 OS 加载程序项启用虚拟机监控程序调试器，请使用 "bcdedit/set <identifier> HYPERVISORDEBUG ON"。

有关标识符的详细信息，请运行 "bcdedit/？ ID "。

## <a name="see-also"></a>另请参阅

[BCDEdit/set](bcdedit--set.md) 命令。

[BCDEdit 选项参考](bcd-boot-options-reference.md)
