---
title: Bug 检查 0x80 NMI_HARDWARE_FAILURE
description: NMI_HARDWARE_FAILURE bug 检查具有 0x00000080 值。 此 bug 检查指示发生了硬件工作不正常。
ms.assetid: 1b376540-d101-44af-8295-d8078a920c67
keywords:
- Bug 检查 0x80 NMI_HARDWARE_FAILURE
- NMI_HARDWARE_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NMI_HARDWARE_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 121fe1dfd53060487ff617106413825b90d4af7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361731"
---
# <a name="bug-check-0x80-nmihardwarefailure"></a>Bug 检查 0x80：NMI\_硬件\_失败


NMI\_硬件\_故障错误检查的值为 0x00000080。 此 bug 检查指示发生了硬件工作不正常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="nmihardwarefailure-parameters"></a>NMI\_硬件\_失败参数


无

<a name="cause"></a>原因
-----

各种硬件故障的影响可能会导致 NMI\_硬件\_故障 bug 检查。 很难确定确切原因。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。 删除任何硬件或最近安装的驱动程序。 请确保所有内存模块都都属于同一类型。

 

 




