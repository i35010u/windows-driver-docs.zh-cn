---
description: 本主题介绍了 Microsoft 提供的用于无自己的 USB 设备类规范的 USB 设备的驱动程序框架。
title: Microsoft 定义的 USB 驱动程序框架
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: a440ab1d829e7fbd85f47bb31e840acd31853ad3
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010261"
---
# <a name="microsoft-defined-usb-driver-frameworks"></a>Microsoft 定义的 USB 驱动程序框架


本主题介绍了 Microsoft 提供的用于无自己的 USB 设备类规范的 USB 设备的驱动程序框架。

Microsoft 为某些类型的 USB 设备提供了驱动程序框架，这些设备没有自己的 USB 设备类规范。 要开发这些类型的设备的供应商应开发一个设备驱动程序，该驱动程序将为设备类型使用指定的框架。

Microsoft 当前为以下 USB 设备提供了以下驱动程序框架：

-   USB 生物识别设备

    Microsoft 通过提供 Windows Biometric Framework)  (指纹读取器支持 USB 生物识别设备。 有关详细信息，请参阅 [生物识别框架概述](/windows/desktop/SecBioMet/biometric-framework-overview)。

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)