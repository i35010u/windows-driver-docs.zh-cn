---
title: 获取 Preparsed 的数据
description: 获取 Preparsed 的数据
ms.assetid: 7a2bdbd1-a970-421f-bbaa-40fe589bb49a
keywords:
- WDK HID，preparsed 数据集合
- HID 的集合 WDK，preparsed 数据
- WDK HID preparsed 的数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 089101113e7099787f7d36d760cc79fb96ced77a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554663"
---
# <a name="obtaining-preparsed-data"></a>获取 Preparsed 的数据





本部分介绍如何在用户模式应用程序和内核模式驱动程序获取的 HID 集合[preparsed 数据](preparsed-data.md)，这是描述集合的不透明结构的 HID 报表。

### <a name="user-mode-application"></a>用户模式应用程序

在用户模式应用程序调用的任何之前必须获取集合的 preparsed 的数据[HIDClass 支持例程](https://msdn.microsoft.com/library/windows/hardware/ff538865)要求将 preparsed 的数据。 应用程序应保留权访问集合的 preparsed 数据，只要它已在设备上打开的文件。

打开文件上的 HID 集合后，应用程序调用[ **HidD\_GetPreparsedData** ](https://msdn.microsoft.com/library/windows/hardware/ff539679)返回集合的 preparsed 例程分配的缓冲区中的数据。

应用程序应调用[ **HidD\_FreePreparsedData** ](https://msdn.microsoft.com/library/windows/hardware/ff538893)应用程序不再需要对集合的访问。

### <a name="kernel-mode-driver"></a>Kernel-Mode Driver

内核模式驱动程序打开 HID 集合后，驱动程序将获取集合的[preparsed 数据](preparsed-data.md)如下所示：

-   获取集合的 preparsed 数据的长度

-   获取集合的 preparsed 的数据

若要确定 preparsed 数据的长度，则驱动程序，请使用[ **IOCTL\_HID\_获取\_集合\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541092)请求。 此请求将返回[ **HID\_集合\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff539870)结构。 **DescriptorSize**此结构的成员指定的大小，以字节为单位的集合的 preparsed 数据。 该驱动程序必须分配从非分页缓冲池的最小此缓冲区大小以容纳 preparsed 的数据。

在为 preparsed 数据分配缓冲区之后, 该驱动程序使用[ **IOCTL\_HID\_获取\_集合\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541089)请求到获取 preparsed 的数据。

获取后 preparsed 的数据，该驱动程序可以用它和**HidP\_**<em>Xxx</em> HID 支持以获取有关功能的 HID 集合的信息并将提取的例程控制 HID 报告中的数据。

 

 




