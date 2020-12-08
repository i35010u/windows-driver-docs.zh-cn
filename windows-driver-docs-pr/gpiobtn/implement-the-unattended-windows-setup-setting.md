---
title: 实现无人参与 Windows 安装程序设置
description: 本主题介绍如何设置无人参与的 Windows 安装程序组件设置。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c47c4a437154431c2008cf818d7459275b6c566
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794977"
---
# <a name="implement-the-unattended-windows-setup-setting"></a>实现无人参与 Windows 安装程序设置


本主题介绍如何设置无人参与的 Windows 安装程序组件设置。

强烈建议使用 [Windows 系统映像管理器](/previous-versions/windows/it-pro/windows-vista/cc722301(v=ws.10)) 编辑 Windows 安装程序的无人参与文件。

下面是一个示例输出文件：

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

 

