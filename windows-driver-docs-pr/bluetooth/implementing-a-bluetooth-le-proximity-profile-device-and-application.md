---
title: 蓝牙 LE 邻近配置文件概述
description: 邻近检测是一个常见用途的蓝牙低能耗 (LE)。
ms.assetid: 4BF27CBE-C89A-48DC-8536-1A5111CDB0C4
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 355aaf293adae94bdbb2e0850c34a5857307261c
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608472"
---
# <a name="bluetooth-le-proximity-profile-overview"></a>蓝牙 LE 邻近配置文件概述


邻近检测是一个常见用途的蓝牙低能耗 (LE)。 Windows 8.1 扩展了 Windows 8 中引入的蓝牙 LE 支持。 本部分提供了准则来创建可用于开发与 Windows 8.1 兼容的 UWP 设备应用程序的邻近性配置文件的设备实现。

开发此应用程序之前，您应熟悉蓝牙 LE 函数和蓝牙 LE 邻近配置文件规范。

## <a name="span-idexampleservicedeclarationspanspan-idexampleservicedeclarationspanspan-idexampleservicedeclarationspanexample-service-declaration"></a><span id="Example_Service_Declaration"></span><span id="example_service_declaration"></span><span id="EXAMPLE_SERVICE_DECLARATION"></span>示例服务声明


蓝牙低能耗引入了新的物理层共享相同的频率空间蓝牙基本速率。 所谓的泛型属性配置文件 （或 GATT） 分为低能耗配置文件。

GATT 配置文件声明一个或多个定义用例或方案的服务。 若要开发符合服务实现，必须将组织*特征*，以便它们定义上的已建立架构符合[蓝牙特别兴趣组 (SIG) 开发人员网站](https://go.microsoft.com/fwlink/p/?linkid=320723).

下图显示了如何*特征*典型 GATT 服务内部结构。

![示例 gatt 服务声明](images/bthleservicedeclaration.png)

示例邻近配置文件中进行了介绍进一步[蓝牙近距离](bluetooth-proximity-profile.md)。

 

 





