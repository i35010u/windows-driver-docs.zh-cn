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
ms.openlocfilehash: a55dbebcc53e18aa328985079a034da07c358c9c
ms.sourcegitcommit: fac288eb2cceb6a7a8248ae0f8086553d1659b23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2019
ms.locfileid: "56588956"
---
# <a name="bug-check-0x80-nmihardwarefailure"></a>Bug 检查 0x80：NMI\_硬件\_失败


NMI\_硬件\_故障错误检查的值为 0x00000080。 此 bug 检查指示发生了硬件工作不正常。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="nmihardwarefailure-parameters"></a>NMI\_硬件\_失败参数


无

<a name="cause"></a>原因
-----

各种硬件故障的影响可能会导致 NMI\_硬件\_故障 bug 检查。 很难确定确切原因。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。 删除任何硬件或最近安装的驱动程序。 请确保所有内存模块都都属于同一类型。

 

 




