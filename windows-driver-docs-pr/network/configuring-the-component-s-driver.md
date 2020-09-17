---
title: 配置组件的驱动程序
description: 配置组件的驱动程序
ms.assetid: 0aab9bb0-180c-4e21-ac8e-f20db7e8201a
keywords:
- 通知对象 WDK 网络，驱动程序配置
- 网络通知对象 WDK，驱动程序配置
- 驱动程序配置 WDK 网络组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 863f9bf15642f924c6376c7a2c0d2e16726b52b7
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716716"
---
# <a name="configuring-the-components-driver"></a>配置组件的驱动程序





网络配置子系统调用通知对象的 [**INetCfgComponentControl：： ApplyPnpChanges**](/previous-versions/windows/hardware/network/ff547726(v=vs.85)) 方法之后，通知对象应将配置信息发送到拥有 notify 对象的网络组件的驱动程序。 网络配置子系统在调用[**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85))方法之后以及特定网络组件的驱动程序和服务启动后，调用**ApplyPnpChanges** 。 在 **ApplyPnpChanges** 调用中，网络配置子系统通过 [**INetCfgPnpReconfigCallback**](/previous-versions/windows/hardware/network/ff547935(v=vs.85)) 接口。 组件的 notify 对象可使用 **INetCfgPnpReconfigCallback** 接口将配置信息发送到组件的驱动程序。 此驱动程序必须是 TDI 提供程序或 NDIS 微型端口驱动程序。

Notify 对象可以在其**ApplyPnpChanges**实现中调用[**INetCfgPnpReconfigCallback：： SendPnpReconfig**](/previous-versions/windows/hardware/network/ff547943(v=vs.85)) ，以将配置信息发送到其组件的驱动程序。 **SendPnpReconfig** 将配置信息传递给驱动程序。

或者，notify 对象可以调用 Win32 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 函数来打开到其组件驱动程序的连接。 Notify 对象可以调用 Win32 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数，以将控制代码和输入数据直接发送到其组件的驱动程序。

通知对象不需要使用 **INetCfgPnpReconfigCallback**。 但如果通知对象使用 **INetCfgPnpReconfigCallback**，则不需要用户重新启动操作系统以使配置更改在驱动程序中生效。

 

