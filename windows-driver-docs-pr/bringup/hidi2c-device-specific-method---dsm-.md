---
title: HIDI2C 的特定于设备的方法 (_DSM)
description: 在 ACPI 5.0 规范中，在9.14.1、\ 0034; _DSM (特定于设备的方法) \ 0034; 中定义 _DSM 方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795652d03dde598e3291930e9a31c66f426bbc13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788981"
---
# <a name="hidi2c-device-specific-method-_dsm"></a> (DSM) 的 HIDI2C Device-Specific 方法 \_


\_ \_ 在[ACPI 5.0 规范](https://uefi.org/specifications)的 "Dsm (设备特定方法) " 部分中定义 DSM 方法。 此方法提供了特定于设备的数据和控制函数，可由设备驱动程序调用，而不会与其他此类特定于设备的方法发生冲突。

\_特定设备或类的 DSM 定义一个 UUID (GUID) ，该保证不会与其他 uuid 冲突。 对于每个 UUID，有一组已定义的函数， \_ DSM 方法可以实现该函数来为驱动程序提供数据或执行控制功能。

对于设备的 HIDI2C 类，函数1定义如下：

### <a name="arguments"></a>自变量

-   **Arg0：** UUID = 3cdff6f7-4267-4555-ad05-b30a3d8938de
-   **Arg1：** 修订版 ID = 1
-   **Arg2：** 函数 index = 1
-   **Arg3：** 内容

### <a name="return"></a>返回

一个包含 HidDescriptorAddress 的整数。 此地址是 I2C 设备中的寄存器偏移量，可以在该设备上读取 HID 描述符 (的) 。
**注意**  每个 DSM 的函数索引 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关详细信息，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)中的 9.14.1 "DSM (设备特定方法) " 部分。

 

 

 




