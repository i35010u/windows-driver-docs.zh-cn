---
title: 选项文件示例
description: 选项文件示例
ms.assetid: 632c37a8-a1cc-419a-917f-94e9308c4993
keywords:
- 选项文件 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c17133f8c4d4e6b88fb858314e915faf970e79f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575257"
---
# <a name="option-file-examples"></a>选项文件示例


**示例 1:更改超时值**

在以下示例 Sdv default.xml 文件中，超时增加到两个小时 （即，7200 秒）。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">7200</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads></SlamConfig>
```

**示例 2:更改 Spaceout 值**

在以下示例 Sdv default.xml 文件中，可供 SDV 虚拟内存增加到了 3500 MB (3.5 GB)。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">3500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads>
</SlamConfig>
```

**示例 3:更改 NumberOfThreads 值**

在以下示例 Sdv default.xml 文件中，可供 SDV 的线程数仅限于 2。

```XML
<?xml version="1.0" encoding="utf-8" ?> 
- <SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout> 
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout> 
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">2</SDV_SlamConfig_NumberOfThreads> 
  </SlamConfig>
```

 

 





