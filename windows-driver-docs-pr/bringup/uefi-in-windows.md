---
title: Windows 中的 UEFI
description: Windows 中的 UEFI
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1155e22a4da08c2681fc9d08996e6a834af4ed31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803641"
---
# <a name="uefi-in-windows"></a>Windows 中的 UEFI

> [!NOTE]
> 本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

Windows 利用统一可扩展固件接口 (UEFI) ，以支持从 SoC 固件启动加载程序到操作系统的系统控制。 UEFI 环境是在其上启动 Windows 设备和操作系统运行的最小启动操作系统。

UEFI 是基于标准 UEFI 规范的启动加载程序的一般框架，它描述了一种标准环境和平台固件的一组接口，使操作系统能够启动。 UEFI 规范可在 [UEFI.org](https://uefi.org/specifications)上找到。由于 UEFI 的级别非常低，其每个实现特定于特定的 SoC。 对于 Windows 设备，由 SoC 供应商提供的核心 UEFI 环境和某些 UEFI 驱动程序。 Microsoft 提供了其他 UEFI 驱动程序和 UEFI 应用程序 (例如闪烁的应用程序) 。

除了 UEFI 规范中所述的实现细节外，还提供了一组额外的 UEFI 要求，用于在 SoC 平台上运行 Windows。 有关这些要求，请参阅 [SoC 平台上 Windows 的最低 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)。

## <a name="in-this-section"></a>在本节中

| 主题 | 描述 |
| --- | --- |
| [SoC 平台上的 Windows 的最低 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md) | 统一可扩展固件接口 (UEFI) 是运行 Windows 的 SoC 平台所需的启动固件。 本部分介绍在 SoC 平台上运行 Windows 的 UEFI 实现要求。 观察和遵循这些要求将有助于确保 Windows 的正确功能。 |
| [Windows 的 UEFI 协议](uefi-protocols-for-windows.md) | 本部分介绍 Windows 定义的 UEFI 协议。 这些协议会向上扩展 UEFI 规范定义的协议，Windows 在启动过程中用于完成特定功能。 |
| [Windows UEFI 固件更新平台](windows-uefi-firmware-update-platform.md) | Windows 支持一个平台，用于通过使用 UEFI UpdateCapsule 函数处理的驱动程序包来安装系统和设备固件更新。 此平台提供一致、可靠的固件更新体验，并改善最终用户的重要系统固件更新的发现。 |

## <a name="uefi-components-for-windows"></a>适用于 Windows 的 UEFI 组件

下图显示了 Windows 设备的主要 UEFI 组件

![适用于 windows phone 的 uefi 组件](images/oem-uefi-components.png)

## <a name="oem-components-in-the-uefi-environment"></a>UEFI 环境中的 OEM 组件

Oem 可以添加 UEFI 应用程序来帮助制造和服务设备。 最终用户无法访问这些应用程序。 面向最终用户的 UEFI 应用程序只能由 Microsoft 实现并由 Windows 启动管理器启动。

选择实现 UEFI 应用程序的 Oem 应确保这些应用程序的内存占用量较小，并且不会影响启动时间。 有关为 UEFI 环境创作组件的详细信息，请咨询 SoC 供应商。

> [!IMPORTANT]
> Oem 可能还需要替换 SoC 供应商提供的特定 UEFI 驱动程序以匹配其特定硬件。 有关详细信息，请跟进 SoC 供应商。

## <a name="related-topics"></a>相关主题

[Windows 的 UEFI 协议](uefi-protocols-for-windows.md)  
