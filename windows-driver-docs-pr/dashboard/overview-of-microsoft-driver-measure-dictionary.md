---
title: Microsoft 驱动程序度量
description: 发布者和作者使用 Microsoft 驱动程序度量的说明来更好地了解 Microsoft 在驱动程序外部测试过程中用于评估驱动程序质量的标准
ms.topic: article
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 86813b4c730ff62fea0f2eeeb2568065178b8bd1
ms.sourcegitcommit: 85a89ea01c5018bc09e508dadaace5e6b428555b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2020
ms.locfileid: "83394011"
---
# <a name="overview-of-the-microsoft-driver-measures"></a>Microsoft 驱动程序度量概述

Microsoft 通过 Windows 更新服务分配成千上万个驱动程序，每月为数百万计算机和用户提供服务。 大规模安全地提供适当驱动程序需要在分配过程中通过实际验证来评估驱动程序质量。

本文档供 Windows 设备驱动程序的发布者和作者参考。  发布者和作者可以更好地了解 Microsoft 在[驱动程序外部测试过程](https://docs.microsoft.com/windows-hardware/drivers/dashboard/driver-flighting)中用于评估驱动程序质量的标准。 熟悉驱动程序质量标准将有助于驱动程序发布者了解 Microsoft 如何决定发布其驱动程序。

使用粗体的关键字在术语表中具有相应的定义。

本内容包含三个部分：

* 使用度量：度量的定义、度量的类型，以及度量如何评估质量。
* [驱动程序度量特性](measure-attributes.md)：定义每个度量所具有的各种特性。
* 驱动程序度量字典：提供每个驱动程序度量（无论是系统还是设备类）的定义，以及说明、特性值和计算逻辑 。

## <a name="using-measures"></a>使用度量

Microsoft 将度量定义为可量化的指标，用于衡量公司所提供的产品的质量。 驱动程序度量聚合客户计算机生成的遥测数据，并处理与驱动程序相关的任何事件。 每个度量的作用域为驱动程序的功能用例，从而确保最终用户可以体验组件的各种功能。

## <a name="types-of-measures"></a>度量的类型

为了评估驱动程序的质量，Microsoft 提供了两种不同类型的度量：系统度量和设备类度量 。

系统度量可确保驱动程序安装无误且计算机仍旧可靠；Microsoft 将这些度量应用于提交的每个驱动程序。 设备类度量监视驱动程序的特定功能，以确保硬件组件按预期方式工作；每个设备类都应用了一组不同度量，或者仅使用系统度量进行评估。

提交给 Microsoft 审批的所有驱动程序都会进行系统质量评估。 系统度量评估计算机的质量和状态，而无需了解驱动程序的特定功能。 当前系统度量监视驱动程序安装是否成功以及计算机的可靠性。 驱动程序安装度量监视在受众中的安装是否成功，并检测任何安装后错误。

当合作伙伴向 Microsoft 提交某一驱动程序时，该驱动程序将与指示该驱动程序适用于哪个组件的设备类相关联。 每个设备类都使用一组不同度量来评估驱动程序在组件上的行为，或者仅使用系统度量进行评估。

## <a name="how-measures-assess-driver-quality"></a>度量如何评估驱动程序质量

每个度量都有自己的计算逻辑，这是一种算法，用于分析与驱动程序相关的事件的遥测数据，并将结果聚合为失败次数与成功次数的百分比、比率或直方图。 此结果是度量的当前值；当前值根据最低质量限度（称为度量的通过标准）计算得来 。

如果某一度量的当前值不满足其通过标准，则该度量将会失败，从而触发可能导致修正的调查，例如外部测试被拒或市场到期。

## <a name="evaluating-by-targeting-cohort"></a>按目标队列评估

可以开发一个驱动程序来支持多个系统和设备。 通过聚合驱动程序在所有目标设备（见下面的目标队列定义）中的度量结果来评估驱动程序的质量，这并不总是足够或准确的。 为了确保没有低性能的目标队列，我们分析这些队列，以发现任何不符合度量要求的队列。 所有驱动程序度量都用于按目标队列评估驱动程序质量，因为它们能够支持按目标队列评估。 请查看每个度量定义页中是否标有新的度量属性 `cohort-capable`。 如果度量被标记为 `cohort-capable`，表示度量能够支持按目标队列评估。

### <a name="targeting-cohortsclusters-definition"></a>目标队列/群集定义
目标队列/群集的定义为，发货标签指定和共用相同的目标属性（包括 HWID、CHID 和 OS 版本）的一组 Windows 系统和设备。

### <a name="cohort-evaluation-passfail-criteria"></a>队列评估通过/未通过条件
如果一个或多个驱动程序度量不符合通过条件，目标队列就不能通过评估（未通过）。 如果在一个或多个目标队列中检测到一个或多个评估未通过，驱动程序可能会遭到拒绝。  启用后，将会把至少所需的队列实例添加到度量定义页。

## <a name="data-sources-for-measures"></a>度量的数据源

为了评估驱动程序质量，度量合并了在两个不同客户组中运行的计算机的数据：Windows 预览体验计划 (WIP) 和零售 。

WIP 数据对于外部测试方案至关重要，因为用户已选择向 Microsoft 提供更高级别的遥测，以供实际验证时使用。 零售数据从常规 Windows 生态系统收集得来，允许 Microsoft 监视已发布驱动程序的质量问题。

## <a name="count-differences-between-measures"></a>度量之间的计数差异

Microsoft 通过唯一计算逻辑、特性集、采样百分比和评估标准，以不同方式构造每个度量。 因此，应用于不同驱动程序的一组度量可能会报告不一致的计数；Microsoft 预期存在这些差异。

## <a name="related-topics"></a>相关主题

[音频度量](audio-measures.md)

[蓝牙度量](bluetooth-measures.md)

[相机度量](camera-measures.md)

[指纹度量](fingerprint-measures.md)

[固件度量](firmware-measures.md)

[显卡度量](graphics-measures.md)

[Wi-Fi 度量](wi-fi-measures.md)

[术语表](measures-glossary.md)
