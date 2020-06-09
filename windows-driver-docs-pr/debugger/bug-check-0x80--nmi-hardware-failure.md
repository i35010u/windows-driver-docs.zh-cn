---
title: Bug 检查 0x80 NMI_HARDWARE_FAILURE
description: NMI_HARDWARE_FAILURE bug 检查的值为0x00000080。 此错误检查表明出现硬件故障。
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
ms.openlocfilehash: ccdd17878cc72c05e7787bf184e35f72ebb40f89
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534802"
---
# <a name="bug-check-0x80-nmi_hardware_failure"></a>Bug 检查0x80： NMI \_ 硬件 \_ 故障


NMI \_ 硬件 \_ 故障 bug 检查的值为0x00000080。 此错误检查表明出现硬件故障。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="nmi_hardware_failure-parameters"></a>NMI \_ 硬件 \_ 故障参数


无

<a name="cause"></a>原因
-----

各种硬件故障可能会导致出现 NMI \_ 硬件 \_ 故障错误检查。 确切的原因很难确定。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 删除最近安装的任何硬件或驱动程序。 请确保所有内存模块的类型相同。

 

 




