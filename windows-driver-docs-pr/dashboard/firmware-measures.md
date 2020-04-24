---
title: 固件度量
description: 固件度量在固件驱动程序外部测试过程中筛选出良性初始化错误
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1e4bbe42d603b3b95b2c0f58ed4c9f8deeffdfb0
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017071"
---
# <a name="firmware-measures"></a>固件度量

Windows 支持平台通过经使用 UEFI Update Capsule 函数进行处理的驱动程序包来安装计算机和设备固件更新，如 [Windows UEFI 固件更新平台](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-uefi-firmware-update-platform)中所述。 UEFI 平台支持计算机级和设备级固件更新，使外部合作伙伴可以安全更新其客户的计算机。 出错的固件包会严重损坏用户的计算机，并导致计算机运行时间更长。
