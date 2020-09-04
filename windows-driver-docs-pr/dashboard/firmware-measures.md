---
title: 固件度量
description: 固件度量在固件驱动程序外部测试过程中筛选出良性初始化错误
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: f99e7d27c1ba6de70b0ac42b30041a2941f635bc
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443871"
---
# <a name="firmware-measures"></a>固件度量

Windows 支持平台通过经使用 UEFI Update Capsule 函数进行处理的驱动程序包来安装计算机和设备固件更新，如 [Windows UEFI 固件更新平台](../bringup/windows-uefi-firmware-update-platform.md)中所述。 UEFI 平台支持计算机级和设备级固件更新，使外部合作伙伴可以安全更新其客户的计算机。 出错的固件包会严重损坏用户的计算机，并导致计算机运行时间更长。