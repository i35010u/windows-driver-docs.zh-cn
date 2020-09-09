---
title: 获取预分析的数据
description: 获取预分析的数据
ms.assetid: 7a2bdbd1-a970-421f-bbaa-40fe589bb49a
keywords:
- 集合 WDK HID，preparsed 数据
- HID 集合 WDK，preparsed 数据
- preparsed 数据 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8de249644d1db0409ae0ff5cd23b207d11849eef
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592393"
---
# <a name="obtaining-preparsed-data"></a>获取预分析的数据





本部分介绍用户模式的应用程序和内核模式驱动程序如何获取 HID 集合的 [preparsed 数据](preparsed-data.md)，这是描述集合的 HID 报表的不透明结构。

### <a name="user-mode-application"></a>用户模式应用程序

在调用需要 preparsed 数据的任何 [HIDClass 支持例程](/windows-hardware/drivers/ddi/index) 之前，用户模式应用程序必须获取集合的 preparsed 数据。 应用程序应保留对集合的 preparsed 数据的访问权限，前提是它在设备上有打开的文件。

打开 HID 集合上的文件后，应用程序将调用 [**HidD \_ GetPreparsedData**](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata) 以在例程分配的缓冲区中返回集合的 preparsed 数据。

当应用程序不再需要访问集合时，应用程序应调用 [**HidD \_ FreePreparsedData**](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_freepreparseddata) 。

### <a name="kernel-mode-driver"></a>内核模式驱动程序

内核模式驱动程序打开 HID 集合后，驱动程序将按以下方式获取集合的 [preparsed 数据](preparsed-data.md) ：

-   获取集合的 preparsed 数据的长度

-   获取集合的 preparsed 数据

为了确定 preparsed 数据的长度，驱动程序将使用 [**IOCTL \_ HID \_ 获取 \_ 集合 \_ 信息**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_information) 请求。 此请求返回一个 [**HID \_ 集合 \_ 信息**](/windows-hardware/drivers/ddi/hidclass/ns-hidclass-_hid_collection_information) 结构。 此结构的 **DescriptorSize** 成员指定集合的 preparsed 数据的大小（以字节为单位）。 驱动程序必须从至少使用此大小的非分页池分配一个缓冲区来保存 preparsed 数据。

为 preparsed 数据分配缓冲区后，驱动程序将使用 [**IOCTL \_ HID \_ 获取 \_ 集合 \_ 描述符**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor) 请求来获取 preparsed 数据。

获取 preparsed 数据后，驱动程序可以将它与**HidP \_ **<em>Xxx</em> HID 支持例程结合使用，以获取有关 hid 集合的功能的信息，并从 hid 报表中提取控件数据。

 

