---
title: 手机网络体系结构和实现
description: 适用于 Windows 10 的移动通信体系结构。
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: aa6a8f2920dae535235cd99e328f469308d4bab2
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248246"
---
# <a name="cellular-architecture"></a>移动通信体系结构

本部分介绍适用于 Windows 10 的移动通信体系结构的元素及其交互方式。 它还包括使蜂窝调制解调器硬件与 Windows 10 兼容的实现要求。

## <a name="windows-10-cellular-architecture"></a>Windows 10 移动电话体系结构

![Windows 10 移动电话体系结构](images/CellularArchitecture.png)

下面介绍 Windows 10 移动版体系结构中显示的元素：

### <a name="user-mode"></a>用户模式 

**WWAN 服务和 MBAE WinRT API** 

无线广域网络服务 (WwanSvc) 负责处理调制解调器初始化、注册、电源状态更改以及自动和手动连接以进行默认和按需移动电话连接。 WWAN 服务还处理 SAR、PCO、Scan、SMS、USSD、LTE 配置、SIM 文件、SIM 卡 PIN 和低级别 SIM 卡访问的调制解调器访问接口。 移动宽带帐户体验 Windows 运行时 (MBAE WinRT) API 允许以编程方式访问原始设备制造商的这些接口， (OEM) /移动运营商 (MO) 应用程序。

**WCM 服务** 

Windows 连接管理器 (WCM) 服务控制 L3 连接，并动态选择哪些特定 L2 介质 (以太网、Wi-fi 或移动电话) 应在任何给定时间连接或断开连接。

**SMS 路由器服务和 SMS WinRT API**
 
SMS 路由器服务负责解码 SMS 数据包数据单元 (PDU) 并将 SMS 消息路由到关联的应用程序。 SMS WinRT API 允许应用程序订阅 SMS 消息，并在接收到匹配消息后启动。 应用还可以发送短信。 在对消息进行解码和可靠传递到服务和应用程序时，SMS 消息会临时存储以进行串联。

**消息服务和消息应用**

消息服务存储用于持久访问的用户短信，应用程序将向用户显示消息。

**LPA (eSIM) 服务和 eSIM WinRT API**

本地配置文件助理 (LPA) 服务通过与订阅管理器（设备预配服务器 (SM +) 进行交互，为用户下载 eSIM 配置文件来实现远程 SIM 配置文件管理的 GSMA 规范。 WinRT API 允许访问 eSIM 配置文件、启用、禁用和删除配置文件，以及通过智能卡界面为固件更新发送低级别应用程序协议数据单元 (APDU) 。

**移动电话 Csp**

移动电话配置服务提供程序 (Csp) 通过 Intune (企业) 、Multivariant 和开放移动联盟来允许配置管理–设备管理和客户端预配 (OMA/CP) 。 Enterprise 使用 EnterpriseAPN、eUICC 和 MultiSIM Csp 替代 APN 连接设置、下载和激活 eSIM 配置文件，并切换到首选 SIM 槽。 CM CellularEntries CSP 用于配置调制解调器的默认连接。 移动电话设置 CSP 用于控制漫游和自动连接配置。 CSPLte 用于 Verizon 特定的配置。

**移动计划服务和移动计划应用**

移动计划服务和应用程序为用户提供了一种简化和安装 eSIM 配置文件的简化机制。

**移动用户 UX**

移动用户 UX 是一种设置应用程序和 VANUI 网络浮出控件，允许用户查看和控制手机网络设置、控制连接和更改无线电状态。 PNIDUI 显示网络的默认网络连接和信号条。 快速操作和飞行模式控制允许无线电状态控制。 

**COSA/MultiVariant 服务**

Country & 操作员设置资产 (COSA) 是一个 OEM 可配置的数据库，其中的设置是通过特定于用户插入的 SIM 的 MultiVariant 服务应用的。 

### <a name="kernel-mode"></a>内核模式

**NDIS**

[ (NDIS) 的网络驱动程序接口规范 ](ndis-drivers.md) 是从网络驱动程序抽象网络硬件并指定分层网络驱动程序之间的标准接口的驱动程序模型。

**NetCx**

[网络适配器 WDF 类扩展 (NetAdapterCx) ](../netcx/index.md) 是提供 WDK 全部功能的驱动程序模型。

**MBBCx**

[Mobile 宽带 WDF Class Extension (MBBCx) ](../netcx/mobile-broadband-mbb-wdf-class-extension-mbbcx.md) 将 NetAdatperCx Driver Framework 扩展为移动设备特定的功能，并实现在不同调制解调器上通用的 "上边缘"。 MbbCx 从 NDIS 处理控件 Oid，并将其转换为 IHV 驱动程序的 MBIM 命令。

**(wmbclass 的 IHV 驱动程序)**


IHV 实现的 "下边缘" 移动设备驱动程序实现了 MBIM 指定的所有特定于适配器的移动电话驱动程序功能。 对于基于 USB 的调制解调器，接口经过标准化并由收件箱 wmbclass 驱动程序处理。 对于 PCIe 移动电话调制解调器设备，IHV 供应商应该提供一个 IHV 客户端驱动程序，用于转换 MBIM 命令以通过 PCIe 总线进行传输。 

### <a name="mbb-and-mbim-driver-interactions"></a>MBB 和 MBIM 驱动程序交互

![windows 10 移动电话体系结构](images/cellular_mbb_driver_architecture.png)

## <a name="windows-10-cellular-implementation-requirements"></a>Windows 10 移动电话实现要求

对于 Windows 10，需要满足以下要求。

-   在调制解调器硬件中实现 MBIM 协议接口。
-   对调制解调器硬件实现 USB 接口。 这可以是可移动的 USB 转换器或其他表现为 USB 主机控制器的接口。

 

 






