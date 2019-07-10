---
title: 获取按用户模式应用程序的 HID 报表
description: 本主题讨论的 HID 输入的报表或 HID 功能报表，获取由用户模式应用程序使用 ReadFile 或 HidD_GetXxx 例程。
ms.assetid: 28f560dd-b919-4652-93f6-691051a0ffbe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0bfa1bfc3766a4122850ea91326c175ae114a6d9
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716807"
---
# <a name="obtaining-hid-reports-by-user-mode-applications"></a>获取按用户模式应用程序的 HID 报表


本主题讨论的 HID 输入的报表或 HID 功能报表，获取用户模式应用程序通过[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)或**HidD\_获取**_Xxx_例程。

但是，应用程序应仅使用**HidD\_获取**_Xxx_例程，从而获取设备的当前状态。 如果应用程序尝试使用[ **HidD\_GetInputReport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getinputreport)持续获取输入的报表，报表可能会丢失。 此外，某些设备可能不支持**HidD\_GetInputReport**，且会变得无响应，如果使用此例程。

以下部分提供的详细信息。

### <a name="using-readfile"></a>使用 ReadFile

应用程序使用打开的文件句柄它通过使用 CreateFile 打开集合上的文件。 当应用程序调用[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)，它无需指定重叠的 I/O，因为[HID 客户端驱动程序](hid-client-drivers.md)缓冲环形缓冲区中的报表。 但是，应用程序可以使用重叠的 I/O 具有多个未完成的读取的请求。

### <a href="" id="using-hid-getxx-routines"></a>使用 HidD\_GetXxx 例程

应用程序可以使用以下[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)以获取最新输入报表和 HID 集合中的功能报表：

<a href="" id="hidd-getinputreport"></a>[**HidD\_GetInputReport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getinputreport)  
输入的报表从 HID 集合返回 （Windows XP 和更高版本）。

<a href="" id="hidd-getfeature"></a>[**HidD\_GetFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getfeature)  
返回从 HID 集合的功能报表。

应用程序可以请求返回特定报表。 若要检索特定报表使用这些例程，该应用程序分配报表输出缓冲区、 缓冲区中，执行零初始化并设置的第一个字节缓冲区中到特定的报表 id。 有关详细信息，请参阅[初始化 HID 报表](initializing-hid-reports.md)。

 

 




