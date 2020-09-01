---
title: 存储端口配置信息
description: 存储端口配置信息
ms.assetid: b1c83729-d7d2-4920-9402-4e00baa12633
keywords:
- 端口管理 WDK 打印，存储配置信息
- 注册表 WDK 打印
- 打印后台处理程序注册表信息 WDK 打印监视器
- 存储打印端口配置信息
- 后台处理程序注册表信息 WDK 打印监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a61fe9f189b6fbce3f67b5622923599b8cb4dc3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214182"
---
# <a name="storing-port-configuration-information"></a>存储端口配置信息





Windows 2000 和更高版本打印后台处理程序可以在群集或非群集服务器环境中运行。 当后台处理程序在服务器群集中运行时，打印监视器配置信息必须存储在群集注册表中。 另一方面，如果后台处理程序在单个非群集服务器系统上运行，则打印监视器配置信息必须存储在服务器的本地注册表中。

打印后台处理程序定义一组用于打印监视器的注册表函数。 这些函数将配置数据定向到适当的注册表，因此打印监视器不必确定服务器是否已群集化。 打印监视器不能直接使用 Win32 注册表 API 或群集注册表 API;所有配置数据都必须使用后台处理程序的注册表功能进行存储和访问。 当后台处理程序调用监视器的[**InitializePrintMonitor2**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)函数时，会将这些函数的地址提供给[**MONITORREG**](/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitorreg)结构中的打印监视器。

在服务器群集中，后台处理程序的多个实例可以共存。 具体而言，每个群集节点都拥有其自己的实例，并且群集本身有一个额外的实例。 后台处理程序注册表函数的输入参数之一是后台处理程序句柄。 此句柄由监视器的 **InitializePrintMonitor2** 函数接收，并标识已打开监视器 (节点或群集) 的后台处理程序实例。 使用后台处理程序的句柄，后台处理程序注册表功能维护每个后台处理程序实例的子项。

 

