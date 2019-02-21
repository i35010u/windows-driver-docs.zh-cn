---
title: 停止后失败的启动设备 (Windows 98 / 我)
description: 停止后失败的启动设备 (Windows 98 / 我)
ms.assetid: 373a1797-6479-4b99-b577-c74494f1774c
keywords:
- 启动 WDK 即插即用失败
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392b9b11e3e59f046a6095c106e76c6a619198ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534189"
---
# <a name="stopping-a-device-after-a-failed-start-windows-98me"></a>停止后失败的启动设备 (Windows 98 / 我)





在 Windows 98 上 / 我，即插即用管理器将发出[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)没有前面的查询时的设备驱动程序失败请求[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 （Windows 2000 及更高版本，即插即用的管理器发送 Irp 中删除这种情况。 请参阅[了解何时删除 Irp 颁发](understanding-when-remove-irps-are-issued.md)。)

在响应停止 IRP，驱动程序版本设备的硬件资源 （例如其 I/O 端口）、 禁用和取消注册任何用户模式接口，和失败要求设备的访问权限的任何传入的 I/O 请求。

 

 




