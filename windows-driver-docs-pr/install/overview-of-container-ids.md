---
title: 容器 ID 概述
description: 容器 ID 概述
ms.assetid: fb7a4a31-01f9-4f7e-a35c-9076c7d73a29
keywords:
- 容器 Id WDK，关于
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc7cadb6c9383a15d7a114dd81fb821254bfa57
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095899"
---
# <a name="overview-of-container-ids"></a>容器 ID 概述


在 Windows 系列操作系统中，设备基本上是功能设备实例的集合，其中每个实例都表示一个功能终结点，该终结点可实现某种形式的设备通信。

术语 " *设备" 节点* (*devnode*) 引用此类功能终结点的 *驱动程序堆栈* ，以及描述终结点及其关联状态的属性。 例如，支持打印机、扫描仪和传真功能的多功能设备可以有多个 devnodes，一个用于设备中的每个功能终结点。

在 Windows 7 之前，每个功能终结点都有一个与之关联的 devnode。 Windows 平台组件和第三方应用程序可查询 devnodes 设备的状态和信息，并可通过功能终结点公开的接口与设备硬件通信。

对于单功能设备，单个 devnode 包含与设备的功能终结点相关的所有信息。 同样，多功能设备具有多个与设备的每个功能终结点相关联的 devnodes。 但是，Windows 无法识别出一组 devnodes 来自同一物理设备。 属于同一多功能设备的每个 devnode 不包含任何标识信息，使即插即用 (PnP) manager 将多个 devnodes 分组为单个设备。 因此，不能对设备和单个物理设备提供的功能进行整体视图。

从 Windows 7 开始，操作系统使用一个新 ID (*容器 ID*) 对源自的一个或多个 devnodes 进行分组，并将其归属到特定物理设备的每个实例。 容器 ID 是每个 devnode 的一个属性，可通过全局唯一标识符 (*GUID*) 值指定。

计算机上安装的物理设备的每个实例都具有唯一的容器 ID。 所有表示物理设备实例上的函数的 devnodes 共享相同的容器 ID。 下图显示了该关系的示例。

![说明多功能设备的容器 id 的关系图 devnodes](images/containerid-1.png)

有一个容器 ID 具有对总线驱动程序的特殊含义： NULL_GUID 定义为： {00000000-0000-0000-0000-000000000000} 。

通常，在报告容器 ID 时不会将 NULL_GUID 作为默认事例返回。 相反，不要处理 BusQueryContainerIDs 情况的 IRP_MN_QUERY_ID，让 PnP 应用其默认逻辑。

当以容器 ID 形式返回 NULL_GUID 时，总线驱动程序将声明为 PnP，设备不得是任何容器的一部分，因此仅在非常特殊的情况下才能返回 NULL_GUID。 例如， *devnode* （如卷设备）可能跨多个容器中的多个磁盘，但不属于任何容器。 此类设备的 [**DEVPKEY_Device_BaseContainerId**](./devpkey-device-basecontainerid.md) 等于 NULL_GUID，它根本没有 [**DEVPKEY_Device_ContainerId**](./devpkey-device-containerid.md) 。

除了非常特殊的情况以外，在报告硬件设备和总线驱动程序时，总线驱动程序绝不应返回 NULL_GUID，这会防止错误的硬件报告其总线的 NULL_GUID 值。 在这些情况下，总线驱动程序应该将此作为设备错误进行威胁，或将其视为设备未报告值。

 

