---
title: 将端口配置信息存储
description: 将端口配置信息存储
ms.assetid: b1c83729-d7d2-4920-9402-4e00baa12633
keywords:
- 端口管理 WDK 打印，存储配置信息
- 注册表 WDK 打印
- 打印后台处理程序注册表信息 WDK 打印监视器
- 存储打印端口配置信息
- 后台处理程序注册表信息 WDK 打印监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdbfa62af0285daa9499bbc89d95945afb6020cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556192"
---
# <a name="storing-port-configuration-information"></a>将端口配置信息存储





Windows 2000 和更高版本的打印后台处理程序可以在运行或者聚集或非聚集服务器环境。 当在服务器群集中运行后台处理程序时，必须群集注册表中存储的打印监视器的配置信息。 但是，如果后台处理程序的单一、 非聚集的服务器系统上操作，打印监视器的配置信息必须存储在服务器的本地注册表。

打印后台处理程序定义了一组注册表函数以供打印监视器。 这些函数配置将数据定向到相应的注册表，因此不需要确定的服务器群集化的打印监视器。 打印监视器必须使用 Win32 注册表 API 或群集注册表 API 直接调用所有配置数据必须存储，并使用后台处理程序的注册表函数访问。 这些函数的地址提供给中的打印监视器[ **MONITORREG** ](https://msdn.microsoft.com/library/windows/hardware/ff557537)结构时后台处理程序调用的监视器[ **InitializePrintMonitor2**](https://msdn.microsoft.com/library/windows/hardware/ff551605)函数。

在服务器群集中，后台处理程序的多个实例可以共存。 具体而言，每个群集节点拥有它自己的实例，并且存在用于群集自身的其他实例。 后台处理程序注册表函数的输入参数之一是后台处理程序句柄。 监视器的接收此句柄**InitializePrintMonitor2**函数，并标识打开了监视器的后台处理程序实例 （节点或群集）。 通过使用后台处理程序句柄，后台处理程序注册表功能维护每个后台处理程序实例的子项。

 

 




