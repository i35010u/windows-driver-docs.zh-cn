---
title: HIDI2C 的特定于设备的方法 (_DSM)
description: 9\.14.1，一节中定义 _DSM 方法 \ 0034; _DSM （设备特定的方法） \ 0034; 在 ACPI 5.0 规范。
ms.assetid: D78077F4-9995-4DC6-9DF6-89D0F8E0C545
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52b9db6c45d295dbe163f4ef358c6b18458ed9e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364541"
---
# <a name="hidi2c-device-specific-method-dsm"></a>HIDI2C 特定于设备的方法 (\_DSM)


\_9.14.1，一节中定义 DSM 方法"\_DSM （设备特定的方法）"，在[ACPI 5.0 规范](https://uefi.org/specifications)。 此方法提供单个、 特定于设备的数据和控制功能可以无冲突其他此类特定于设备的方法调用的设备驱动程序。

\_DSM 为特定设备或类定义保证不与其他 Uuid 冲突 UUID (GUID)。 对于每个 UUID，没有一组已定义的函数的\_DSM 方法可以实现以提供数据或执行的驱动程序控制功能。

对于设备 HIDI2C 类，函数定义，如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** UUID = 3cdff6f7-4267-4555-ad05-b30a3d8938de
-   **Arg1:** 修订 ID = 1
-   **Arg2:** 函数索引 = 1
-   **Arg3:** 无

### <a name="return"></a>返回

包含 HidDescriptorAddress 的整数。 此地址是可以读取 HID descriptor(s) I2C 设备中的偏移量的寄存器。
**请注意**  函数索引为 0 的每个\_DSM 是返回集支持的函数的索引，并始终是必需的查询函数。 有关详细信息，请参阅部分 9.14.1，"\_DSM （设备特定的方法）"，在[ACPI 5.0 规范](https://uefi.org/specifications)。

 

 

 




