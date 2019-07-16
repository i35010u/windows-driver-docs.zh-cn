---
title: 打印机 INF 文件的即插即用 ID
description: 打印机 INF 文件的即插即用 ID
ms.assetid: 4adb9203-1267-466e-89d8-63988ffa56e9
keywords:
- INF 文件 WDK 打印，插 Id
- 即插即用 ID WDK 打印
- 插 Id WDK 打印
- 标识符 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17bb9ee5619d8d224b7f179c192f409e5ecadb7f
ms.sourcegitcommit: 707739250ebdcd74a26d85d8b4217fa81c9c9e95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68181251"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>打印机 INF 文件的即插即用 ID

必须指定[插](plug-and-play-for-printers.md)(PnP) 中的标识符 (Id)[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)。

下表，具体取决于打印机使用的协议中，您必须使用 Id。

|Protocol|打印机 INF 文件中的即插即用 ID。|
|----|----|
|IEEE 1394|该 ID 始终是特定的具有 ID 字符串中的"1394"。|
|并行|该 ID 的 ID 字符串中包含"LPTENUM"。|
|USB|该 ID 的 ID 字符串中包含"USBPRINT"。|
|Dot4|该 ID 的 ID 字符串中包含"DOT4PRT"。 此 ID 适用于 Dot4USB 和并行。|
|蓝牙|该 ID 的 ID 字符串中包含"BTHPRINT"。|
|WSD|该 ID 的 ID 字符串中包含"WSDPRINT"。|
