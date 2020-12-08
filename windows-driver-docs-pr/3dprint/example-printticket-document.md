---
title: PrintTicket 文档示例
description: 本示例中的关键字仅用于说明，尽管它们反映了用于3D 制造的打印架构关键字。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a5a81129e09e4559b0c490bc42ae273bc56f31d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783615"
---
# <a name="printticket-document-example"></a>PrintTicket 文档示例


本示例中的关键字仅用于说明，尽管它们反映了用于3D 制造的打印架构关键字。 此 PrintTicket 专门针对 [PrintCapabilities 文档示例](example-printcapabilities-document.md)所表示的假设设备进行构造。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<psf:PrintTicket
    xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema" version="1"
    xmlns:ns0000="https://schemas.microsoft.com/windows/printing/oemdriverpt/3dprinter"
    xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:vnd="https://foo">

    <psf:ParameterInit name="vnd:Job3DAMap">
        <psf:Value xsi:type="xsd:string">1:0</psf:Value>
    </psf:ParameterInit>
    <psf:ParameterInit name="vnd:Job3DBMap">
        <psf:Value xsi:type="xsd:string">1:1</psf:Value>
    </psf:ParameterInit>

    <psf:Feature name="psk3d:Job3DSupports">
        <psf:Option name="psk3d:SupportsIncluded" />
    </psf:Feature>
    <psf:ParameterInit name="psk3d:Job3DSupportsMaterial">
        <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
    </psf:ParameterInit>

    <psf:Feature name="psk3d:Job3DRaft">
        <psf:Option name="psk3d:RaftIncluded" />
    </psf:Feature>
    <psf:ParameterInit name="psk3d:Job3DRaftMaterial">
        <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
    </psf:ParameterInit>

    <psf:Feature name="psk3d:Job3DQuality">
        <psf:Option name="psk3d:Medium" />
    </psf:Feature>
    <psf:Feature name="psk3d:Job3DDensity">
        <psf:Option name="psk3d:Low"/>
    </psf:Feature>
    
</psf:PrintTicket>
```

 

 




