---
title: 配置组件的驱动程序
description: 配置组件的驱动程序
ms.assetid: 0aab9bb0-180c-4e21-ac8e-f20db7e8201a
keywords:
- 通知对象 WDK 网络驱动程序配置
- 网络通知对象 WDK，驱动程序配置
- 驱动程序配置 WDK 网络组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9cd025e96efd0694f6eff539f81686def1e8364
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374979"
---
# <a name="configuring-the-components-driver"></a>配置组件的驱动程序





在网络后配置子系统调用通知对象的[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))方法，通知对象应配置将信息发送到的驱动程序通知对象所属的网络组件。 网络配置子系统调用**ApplyPnpChanges**它调用后[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))方法和驱动程序之后，特定的网络组件的服务已启动。 在中**ApplyPnpChanges**调用中，网络配置子系统将传递[ **INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))接口。 组件的通知对象可使用**INetCfgPnpReconfigCallback**接口以便将配置信息发送到组件的驱动程序。 此驱动程序必须是 TDI 提供程序或 NDIS 微型端口驱动程序。

通知对象可以调用[ **INetCfgPnpReconfigCallback::SendPnpReconfig** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547943(v=vs.85))内其**ApplyPnpChanges**实现，以配置将信息发送到其组件的驱动程序。 **SendPnpReconfig**将配置信息传递给驱动程序。

或者，通知对象可以调用 Win32 [ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数打开连接到其组件的驱动程序。 通知对象可以调用 Win32 [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数以及输入的数据的控制代码将直接发送到其组件的驱动程序。

通知对象不需要使用**INetCfgPnpReconfigCallback**。 但是，如果通知对象使用**INetCfgPnpReconfigCallback**，用户不必重新启动操作系统，若要使配置更改驱动程序中才会生效。

 

 





