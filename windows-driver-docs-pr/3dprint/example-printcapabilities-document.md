---
title: PrintCapabilities 文档示例
description: 下面的示例中使用的关键字仅用于说明，不过它们通常符合3D 制造的打印架构关键字。
ms.assetid: 0FCEFC25-C22F-44BD-9693-B3DBE6F6D314
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d17fcf00c019f7240648a1188b1328cc95a8ab5
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652751"
---
# <a name="printcapabilities-document-example"></a>PrintCapabilities 文档示例


下面的示例中使用的关键字仅用于说明，不过它们通常符合3D 制造的打印架构关键字。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<psf:PrintCapabilities
    xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema" version="1"
    xmlns:ns0000="https://schemas.microsoft.com/windows/printing/oemdriverpt/3dprinter"
    xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:vnd="https://foo">

    <psf:Property name="psk3d:Job3DOutputArea">
        <psf:Property name="psk3d:Job3DOutputAreaWidth">
            <psf:Value xsi:type="xsd:integer">150000</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DOutputAreaDepth">
            <psf:Value xsi:type="xsd:integer">150000</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DOutputAreaHeight">
            <psf:Value xsi:type="xsd:integer">150000</psf:Value>
        </psf:Property>
    </psf:Property>

    <psf:Property name="psk3d:Job3DKnownObjectTypes">
        <psf:Value xsi:type="xsd:QName">psk3d:MeshOnly</psf:Value>
    </psf:Property>

    <psf:Property name="psk3d:Job3DMaterialCount">
        <psf:Value xsi:type="xsd:integer">5</psf:Value>
    </psf:Property>
    <psf:Property name="psk3d:Job3DMaterials">
        <psf:Property name="vnd:A">
            <psf:Property name="psk:DisplayName">
                <psf:Value xsi:type="xsd:string">Material A</psf:Value>
            </psf:Property>
            <psf:Property name="psk3d:MaterialColor">
                <psf:Value xsi:type="xsd:string">#FFFFFFFF</psf:Value>
            </psf:Property>
        </psf:Property>
        <psf:Property name="vnd:B">
            <psf:Property name="psk:DisplayName">
                <psf:Value xsi:type="xsd:string">Material B</psf:Value>
            </psf:Property>
            <psf:Property name="psk3d:MaterialColor">
                <psf:Value xsi:type="xsd:string">#FF000000</psf:Value>
            </psf:Property>
        </psf:Property>
        <psf:Property name="vnd:C">
            <psf:Property name="psk:DisplayName">
                <psf:Value xsi:type="xsd:string">Material C</psf:Value>
            </psf:Property>
            <psf:Property name="psk3d:MaterialColor">
                <psf:Value xsi:type="xsd:string">#FF000000</psf:Value>
            </psf:Property>
        </psf:Property>
        <psf:Property name="vnd:D">
            <psf:Property name="psk:DisplayName">
                <psf:Value xsi:type="xsd:string">Material D</psf:Value>
            </psf:Property>
            <psf:Property name="psk3d:MaterialColor">
                <psf:Value xsi:type="xsd:string">#FF000000</psf:Value>
            </psf:Property>
        </psf:Property>
        <psf:Property name="vnd:E">
            <psf:Property name="psk:DisplayName">
                <psf:Value xsi:type="xsd:string">Material E</psf:Value>
            </psf:Property>
            <psf:Property name="psk3d:MaterialColor">
                <psf:Value xsi:type="xsd:string">#FF000000</psf:Value>
            </psf:Property>
        </psf:Property>
    </psf:Property>
    
    <psf:ParameterDef name="vnd:Job3DAMap">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DMaterialSelected">
            <psf:Value xsi:type="xsd:QName">vnd:A</psf:Value>
        </psf:Property>
    </psf:ParameterDef>
    <psf:ParameterDef name="vnd:Job3DBMap">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DMaterialSelected">
            <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
        </psf:Property>
    </psf:ParameterDef>
    <psf:ParameterDef name="vnd:Job3DCMap">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DMaterialSelected">
            <psf:Value xsi:type="xsd:QName">vnd:C</psf:Value>
        </psf:Property>
    </psf:ParameterDef>
    <psf:ParameterDef name="vnd:Job3DDMap">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DMaterialSelected">
            <psf:Value xsi:type="xsd:QName">vnd:D</psf:Value>
        </psf:Property>
    </psf:ParameterDef>
    <psf:ParameterDef name="vnd:Job3DEMap">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:Job3DMaterialSelected">
            <psf:Value xsi:type="xsd:QName">vnd:E</psf:Value>
        </psf:Property>
    </psf:ParameterDef>

    <psf:Feature name="psk3d:Job3DQuality">
        <psf:Property name="SelectionType">
            <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
        </psf:Property>
        <psf:Option name="psk3d:Draft" />
        <psf:Option name="psk3d:Medium" />
        <psf:Option name="psk3d:High" />
    </psf:Feature>

    <psf:Feature name="psk3d:Job3DDensity">
        <psf:Property name="SelectionType">
            <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
        </psf:Property>
        <psf:Option name="psk3d:Hollow"/>
        <psf:Option name="psk3d:Low"/>
        <psf:Option name="psk3d:Medium"/>
        <psf:Option name="psk3d:High"/>
        <psf:Option name="psk3d:Solid"/>
    </psf:Feature>

    <psf:Feature name="psk3d:Job3DSupports">
        <psf:Property name="SelectionType">
            <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
        </psf:Property>
        <psf:Option name="psk3d:SupportsIncluded" />
        <psf:Option name="psk3d:SupportsExcluded" />
    </psf:Feature>

    <psf:ParameterDef name="psk3d:Job3DSupportsMaterial">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:QName</psf:Value>
        </psf:Property>
        <psf:Property name="psf:DefaultValue">
            <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
    </psf:ParameterDef>

    <psf:Feature name="psk3d:Job3DRaft">
        <psf:Property name="SelectionType">
            <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
        </psf:Property>
        <psf:Option name="psk3d:RaftIncluded" />
        <psf:Option name="psk3d:RaftExcluded" />
    </psf:Feature>

    <psf:ParameterDef name="psk3d:Job3DRaftMaterial">
        <psf:Property name="psf:DataType">
            <psf:Value xsi:type="xsd:QName">xsd:QName</psf:Value>
        </psf:Property>
        <psf:Property name="psf:DefaultValue">
            <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MaxLength">
            <psf:Value xsi:type="xsd:integer">1024</psf:Value>
        </psf:Property>
        <psf:Property name="psf:MinLength">
            <psf:Value xsi:type="xsd:integer">1</psf:Value>
        </psf:Property>
        <psf:Property name="psf:Mandatory">
            <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
        </psf:Property>
        <psf:Property name="psf:UnitType">
            <psf:Value xsi:type="xsd:string">characters</psf:Value>
        </psf:Property>
    </psf:ParameterDef>

</psf:PrintCapabilities>
```

 

 




