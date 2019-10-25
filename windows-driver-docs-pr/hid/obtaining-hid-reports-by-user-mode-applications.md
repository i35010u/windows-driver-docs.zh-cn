---
title: 通过用户模式应用程序获取 HID 报表
description: 本主题介绍了如何通过使用 ReadFile 或 HidD_GetXxx 例程的用户模式应用程序获取 HID 输入报告或 HID 功能报告。
ms.assetid: 28f560dd-b919-4652-93f6-691051a0ffbe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ee38b45236cd9590fe66cef591b9d8b29dcf0d8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841566"
---
# <a name="obtaining-hid-reports-by-user-mode-applications"></a>通过用户模式应用程序获取 HID 报表


本主题介绍了如何通过使用[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)或**HidD\_获取**_Xxx_例程的用户模式应用程序获取 hid 输入报告或 hid 功能报告。

但是，应用程序应该只使用**HidD\_获取**_Xxx_例程来获取设备的当前状态。 如果应用程序尝试使用[**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)连续获取输入报告，则报告可能会丢失。 此外，某些设备可能不支持**HidD\_GetInputReport**，如果使用此例程，则不会响应。

以下各节提供了详细信息。

### <a name="using-readfile"></a>使用 ReadFile

应用程序使用 CreateFile 获取的打开文件句柄，以打开集合中的文件。 当应用程序调用[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)时，无需指定重叠 i/o，因为[HID 客户端驱动程序](hid-client-drivers.md)会将报告缓冲到环形缓冲区中。 但是，应用程序可以使用重叠 i/o 来具有多个未完成的读取请求。

### <a href="" id="using-hid-getxx-routines"></a>使用 HidD\_GetXxx 例程

应用程序可以使用以下[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)从 HID 集合中获取最新的输入报告和功能报告：

<a href="" id="hidd-getinputreport"></a>[**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)  
从 HID 集合（Windows XP 及更高版本）返回输入报告。

<a href="" id="hidd-getfeature"></a>[**HidD\_GetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getfeature)  
从 HID 集合返回功能报告。

应用程序可以请求特定报表的返回。 若要使用这些例程检索特定报表，应用程序需要分配报表输出缓冲区，并将缓冲区初始化为零，并将缓冲区中的第一个字节设置为特定的报表 ID。 有关详细信息，请参阅[初始化 HID 报表](initializing-hid-reports.md)。

 

 




