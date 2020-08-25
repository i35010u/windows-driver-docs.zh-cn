---
title: 选项文件示例
description: 选项文件示例
ms.assetid: 632c37a8-a1cc-419a-917f-94e9308c4993
keywords:
- 选项文件 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ec42a17f74d3be89ba4b8aa3f4e0d9d030ded2a
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802509"
---
# <a name="option-file-examples"></a>选项文件示例

## <a name="example-1-change-the-timeout-value"></a>示例1：更改超时值

在以下示例 Sdv-default.xml 文件中，超时值将增加到两小时 (，即7200秒) 。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">7200</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads></SlamConfig>
```

## <a name="example-2-change-the-spaceout-value"></a>示例2：更改 Spaceout 值

在以下示例 Sdv-default.xml 文件中，可用于 SDV 的虚拟内存将增加到 3500 MB (3.5 GB) 。

```XML
<?xml version="1.0" encoding="utf-8"?>
<SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">3500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">0</SDV_SlamConfig_NumberOfThreads>
</SlamConfig>
```

## <a name="example-3-change-the-numberofthreads-value"></a>示例3：更改 NumberOfThreads 值

在下面的示例 Sdv-default.xml 文件中，SDV 的可用线程数限制为2。

```XML
<?xml version="1.0" encoding="utf-8" ?>
- <SlamConfig xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <SDV_SlamConfig_Timeout xmlns="http://www.microsoft.com/SDV">3000</SDV_SlamConfig_Timeout>
  <SDV_SlamConfig_Spaceout xmlns="http://www.microsoft.com/SDV">2500</SDV_SlamConfig_Spaceout>
  <SDV_SlamConfig_NumberOfThreads xmlns="http://www.microsoft.com/SDV">2</SDV_SlamConfig_NumberOfThreads>
  </SlamConfig>
```
