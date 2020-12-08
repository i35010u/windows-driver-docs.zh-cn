---
title: Bug 检查 0xE0 ACPI_BIOS_FATAL_ERROR
description: ACPI_BIOS_FATAL_ERROR bug 检查的值为0x000000E0。 这表明某个计算机组件有问题。
keywords:
- Bug 检查 0xE0 ACPI_BIOS_FATAL_ERROR
- ACPI_BIOS_FATAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ACPI_BIOS_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdccd2dd5da84b04e09ec560dcdb3f831e25e66b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816413"
---
# <a name="bug-check-0xe0-acpi_bios_fatal_error"></a>Bug 检查0xE0： ACPI \_ BIOS \_ \_ 错误


ACPI \_ BIOS \_ \_ 错误错误检查的值为0x000000E0。 这表明某个计算机组件有问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="acpi_bios_fatal_error-parameters"></a>ACPI \_ BIOS \_ \_ 错误参数


此 bug 检查的参数由 BIOS （而不是 Windows）发出。 它们只能由硬件供应商来解释。

<a name="cause"></a>原因
-----

计算机的 BIOS 报告系统中的某个组件出现故障，因此 Windows 无法进行操作。 BIOS 指示没有替代方法，但要发出 bug 检查。

<a name="resolution"></a>解决方法
----------

您可以通过运行您的计算机附带的诊断磁盘或工具来确定哪个组件发生了故障。

如果你没有此工具，则必须与系统供应商联系，并向其报告此错误消息。 他们将能够帮助您更正此硬件问题。 这使 Windows 能够正常运行。

Microsoft 无法处理此错误。 只有硬件供应商有资格对其进行分析。

 

 




