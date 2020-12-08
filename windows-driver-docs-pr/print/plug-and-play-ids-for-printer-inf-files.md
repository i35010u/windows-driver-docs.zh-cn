---
title: 打印机 INF 文件的即插即用 ID
description: 打印机 INF 文件的即插即用 ID
keywords:
- INF 文件 WDK 打印，即插即用 Id
- PnP ID WDK 打印
- 即插即用 Id WDK 打印
- 标识符 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb96d84df49532c840162effe4499bd583756323
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807573"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>打印机 INF 文件的即插即用 ID

必须在 "[打印机 INF 文件安装" 部分](printer-inf-file-install-sections.md)中指定[即插即用](plug-and-play-for-printers.md) (PnP) 标识符 (id) 。

您必须根据打印机使用的协议使用下表中的 Id。

|协议|打印机 INF 文件中的 PnP ID。|
|----|----|
|IEEE 1394|ID 始终是特定的，ID 字符串中包含 "1394"。|
|并行程序|ID 字符串中包含 "LPTENUM"。|
|USB|ID 字符串中包含 "USBPRINT"。|
|Dot4|ID 字符串中包含 "DOT4PRT"。 此 ID 适用于 Dot4USB 和 parallel。|
|蓝牙|ID 字符串中包含 "BTHPRINT"。|
|关于|ID 字符串中包含 "WSDPRINT"。|
