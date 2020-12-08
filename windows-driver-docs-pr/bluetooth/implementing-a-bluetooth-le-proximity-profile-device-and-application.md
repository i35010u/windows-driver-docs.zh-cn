---
title: 蓝牙 LE 邻近感应配置文件概述
description: 邻近检测是蓝牙低能耗 (LE) 的常见用法。
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2d5101adb439d88c5394daeea078987efa8e766b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798541"
---
# <a name="bluetooth-le-proximity-profile-overview"></a>蓝牙 LE 邻近感应配置文件概述


邻近检测是蓝牙低能耗 (LE) 的常见用法。 Windows 8.1 扩展了 Windows 8 中引入的蓝牙 LE 支持。 本部分提供了一些准则，用于创建邻近感应配置文件的设备实现，可用于开发与 Windows 8.1 兼容的 UWP 设备应用。

在开发此应用程序之前，你应该熟悉蓝牙 LE 功能和蓝牙 LE 近程配置文件规范。

## <a name="span-idexample_service_declarationspanspan-idexample_service_declarationspanspan-idexample_service_declarationspanexample-service-declaration"></a><span id="Example_Service_Declaration"></span><span id="example_service_declaration"></span><span id="EXAMPLE_SERVICE_DECLARATION"></span>服务声明示例


蓝牙低能耗引入了一个新的物理层，它与蓝牙基本速度共享相同的频率空间。 低能耗配置文件被组织成了所谓的泛型属性配置文件 (或 GATT) 。

GATT 配置文件声明一个或多个定义用例或方案的服务。 若要开发兼容的服务实现，你必须组织 *特征* ，使其符合在 [蓝牙特别兴趣组 (SIG) 开发人员网站](https://go.microsoft.com/fwlink/p/?linkid=320723)上定义的已建立架构。

此图显示了如何在典型的 GATT 服务内构造 *特征* 。

![gatt 服务声明示例](images/bthleservicedeclaration.png)

[蓝牙邻近配置文件](bluetooth-proximity-profile.md)中进一步介绍了有关邻近配置文件的示例。

 

 





