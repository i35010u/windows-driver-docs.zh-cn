---
title: 实现无人参与 Windows 安装程序设置
description: 本主题介绍如何设置无人参与的 Windows 安装程序组件设置。
ms.assetid: 593F8E05-F886-45FE-83EB-8DDD204F7900
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 392db897c42d4a96d02874f84e0a54e286a8ca12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323416"
---
# <a name="implement-the-unattended-windows-setup-setting"></a>实现无人参与 Windows 安装程序设置


本主题介绍如何设置无人参与的 Windows 安装程序组件设置。

我们强烈建议你使用[Windows 系统映像管理器](https://go.microsoft.com/fwlink/p/?linkid=324691)编辑无人参与的 Windows 安装程序文件。

下面是示例输出文件：

``` syntax
<unattend xmlns="urn:schemas-microsoft-com:unattend">
  <settings pass="specialize">
    <component
        name="Microsoft-Windows-GPIOButtons"
        processorArchitecture="x86"> <!-- ... Additional component attributes-->
      <ConvertibleSlateMode>1</ConvertibleSlateMode> <!-- Values: {0 (slate); 1 (laptop)}-->
    </component>
  </settings>
</unattend>
```

 

 




