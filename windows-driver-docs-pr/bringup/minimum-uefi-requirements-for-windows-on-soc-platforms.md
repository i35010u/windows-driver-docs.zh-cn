---
title: SoC 平台上的 Windows 的最低 UEFI 要求
description: SoC 平台上的 Windows 的最低 UEFI 要求
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: cfeb85e2dc6b5ecde3186960963f3a8da252bb09
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784189"
---
# <a name="minimum-uefi-requirements-for-windows-on-soc-platforms"></a>SoC 平台上的 Windows 的最低 UEFI 要求

统一可扩展固件接口 (UEFI) 是运行 Windows 的 SoC 平台所需的启动固件。 本部分介绍在 SoC 平台上运行 Windows 的 UEFI 实现要求。 观察和遵循这些要求将有助于确保 Windows 的正确功能。

这组要求适用于任何基于 SoC 的计算系统，但有一些限制。 本指南假定已满 Windows 功能集，并支持传统的 netbook 形式因素和无线、仅多点触控移动设备。 因此，它将自身局限于预计在此类系统上广泛使用的技术。 对于实现本文档未涵盖的技术的系统，请参阅 [uefi 规范](https://uefi.org/specifications)中的 uefi 规范。

Windows 支持基于统一可扩展固件接口 (UEFI) 版本2.3.1 或更高版本的固件修订版本。

> [!NOTE]
> Windows 支持在 UEFI 2.3.1 规范中定义的一小部分功能。 对于更高版本的固件，Windows 实现没有显式检查。 如果操作系统包含本文档中所述的必要支持，则操作系统将支持更高版本的固件。

## <a name="in-this-section"></a>在本节中

| 主题 | 描述 |
| --- | --- |
| [适用于 SoC 平台上的所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md) | 介绍适用于适用于 Windows 10 的 UEFI 要求 (家庭、专业版、企业版和教育版) 以及 Windows 10 移动版。 |
| [Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md) | 运行 Windows 10 移动版的设备必须满足本主题中所述的其他要求。 |
| [USB 刷写支持的 UEFI 要求](uefi-requirements-for-usb-flashing-support.md) | Microsoft 提供了多个基于 USB 的闪烁解决方案，可用于工程环境和生产环境。 为了使设备与这些工具一起使用，设备上的 UEFI 环境必须满足本主题中列出的要求。 |
