---
title: 启动失败后停止设备 (Windows 98/Me)
description: 启动失败后停止设备 (Windows 98/Me)
ms.assetid: 373a1797-6479-4b99-b577-c74494f1774c
keywords:
- 未能启动 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8168c3204831a0a68514d7771919b83a626453eb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184745"
---
# <a name="stopping-a-device-after-a-failed-start-windows-98me"></a>启动失败后停止设备 (Windows 98/Me)





在 Windows 98/Me 上，当设备的驱动程序无法使用[**irp \_ MN \_ 开始 \_ 设备**](./irp-mn-start-device.md)请求时，PnP 管理器会发出[**irp \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md)请求，但不执行上述查询。  (在 Windows 2000 和更高版本上，PnP 管理器会在这种情况下发送删除 Irp。 请参阅 [了解何时发出删除 irp](understanding-when-remove-irps-are-issued.md)。 ) 

为了响应停止 IRP，驱动程序会释放设备的硬件资源 (如) 的 i/o 端口，禁用并取消注册任何用户模式接口，并失败需要访问设备的任何传入 i/o 请求。

 

