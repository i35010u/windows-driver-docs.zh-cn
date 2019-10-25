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
ms.openlocfilehash: c9aae43356ab04ba29c30acbca322ca4570fb8f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844412"
---
# <a name="storing-port-configuration-information"></a>存储端口配置信息





Windows 2000 和更高版本打印后台处理程序可以在群集或非群集服务器环境中运行。 当后台处理程序在服务器群集中运行时，打印监视器配置信息必须存储在群集注册表中。 另一方面，如果后台处理程序在单个非群集服务器系统上运行，则打印监视器配置信息必须存储在服务器的本地注册表中。

打印后台处理程序定义一组用于打印监视器的注册表函数。 这些函数将配置数据定向到适当的注册表，因此打印监视器不必确定服务器是否已群集化。 打印监视器不能直接使用 Win32 注册表 API 或群集注册表 API;所有配置数据都必须使用后台处理程序的注册表功能进行存储和访问。 当后台处理程序调用监视器的[**InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)函数时，会将这些函数的地址提供给[**MONITORREG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitorreg)结构中的打印监视器。

在服务器群集中，后台处理程序的多个实例可以共存。 具体而言，每个群集节点都拥有其自己的实例，并且群集本身有一个额外的实例。 后台处理程序注册表函数的输入参数之一是后台处理程序句柄。 此句柄由监视器的**InitializePrintMonitor2**函数接收，并标识已打开监视器的假脱机程序实例（节点或群集）。 使用后台处理程序的句柄，后台处理程序注册表功能维护每个后台处理程序实例的子项。

 

 




