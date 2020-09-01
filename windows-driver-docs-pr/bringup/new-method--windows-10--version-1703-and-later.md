---
title: 新方法-Windows 10 版本1703及更高版本
description: 新方法-Windows 10 版本1703及更高版本
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f158adb2de0e3ee27953f72a613bc3d32806103
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189405"
---
# <a name="new-method---windows-10-version-1703-and-later"></a>新方法-Windows 10 版本1703及更高版本


Microsoft 创建了一个新的 Mbr2gpt.exe 工具，可用于在非破坏性转换中将旧的 MBR 磁盘转换为 GPT 磁盘。

[MBR2GPT.exe](/windows/deployment/mbr-to-gpt) 有助于以非破坏性方式在合格系统上从旧的 BIOS 配置迁移到完整的 UEFI。

先前的方法被视为破坏性转换，因为技术人员、应用程序或进程必须在将磁盘转换为 GPT 磁盘之前擦除该磁盘。